<template>
  <div
    class="square"
    :style="{
      backgroundColor: square.flipped || square.matched ? square.color : 'gray',
    }"
    @click="$emit('flip')"
  ></div>
</template>

<script>
export default {
  props: ['square'],
};
</script>

<style scoped>
.square {
  width: 100px;
  height: 100px;
  background-color: gray;
  border: 1px solid #ccc;
  cursor: pointer;
  transition: background-color 0.3s;
}
.square:hover {
  opacity: 0.8;
}
</style>
