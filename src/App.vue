<template>
  <div class="memory-game">

    <div class="grid">
      <Square
        v-for="(square, index) in squares"
        :key="index"
        :square="square"
        @flip="flipSquare(index)"
      />
    </div>

  </div>
</template>

<script>
import Square from './components/Square.vue';

export default {
  components: { Square },
  data() {
    return {
      squares: [],
      flippedIndexes: [],
      isGameOver: false,
    };
  },
  methods: {
    initializeGame() {
      const colors = [
        'red',
        'blue',
        'green',
        'yellow',
        'orange',
        'purple',
        'pink',
        'cyan',
      ];
      const doubledColors = [...colors, ...colors];
      this.squares = doubledColors
        .sort(() => 0.5 - Math.random())
        .map((color) => ({ color, flipped: false, matched: false }));
    },
    flipSquare(index) {
      const square = this.squares[index];

      if (
        square.matched ||
        square.flipped ||
        this.flippedIndexes.length === 2
      ) {
        return;
      }

      square.flipped = true;
      this.flippedIndexes.push(index);

      if (this.flippedIndexes.length === 2) {
        const [firstIndex, secondIndex] = this.flippedIndexes;
        const firstSquare = this.squares[firstIndex];
        const secondSquare = this.squares[secondIndex];

        if (firstSquare.color === secondSquare.color) {
          firstSquare.matched = true;
          secondSquare.matched = true;
        } else {
          setTimeout(() => {
            firstSquare.flipped = false;
            secondSquare.flipped = false;
          }, 1000);
        }

        this.flippedIndexes = [];
      }

      this.isGameOver = this.squares.every((square) => square.matched);
    },
  },
  created() {
    this.initializeGame();
  },
};
</script>

<style>
.memory-game {
  text-align: center;
  font-family: Arial, sans-serif;
}
.grid {
  display: grid;
  grid-template-columns: repeat(4, 100px);
  grid-gap: 10px;
  justify-content: center;
  margin: 20px auto;
}
</style>
