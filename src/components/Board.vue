<template>
  <div class="grid">
    <Square
      v-for="(square, index) in squares"
      :key="index"
      :square="square"
      @flip="flipSquare(index)"
    />
  </div>
</template>

<script>
import Square from './Square.vue';

export default {
  components: { Square },
  props: ['squares', 'flipSquare'],
};
</script>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(4, 100px);
  grid-gap: 10px;
  justify-content: center;
  margin: 20px auto;
}
</style>
