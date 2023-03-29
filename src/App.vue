<template>
  <div class="app">
    <board-component :board="board" />
  </div>  

</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { Board } from './models/Board';
import BoardComponent from './components/BoardComponent.vue';

const board = ref();

function restart() {
  const newBoard = new Board();
  newBoard.initCells();
  newBoard.addFigures();
  board.value = newBoard;
}

onMounted(() => {
  restart();
})
</script>

<style lang="scss" scoped>
  * {
    padding: 0;
    margin: 0;
  }
  .app {
    padding: 0;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
