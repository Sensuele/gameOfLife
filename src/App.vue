<template>
  <div class="app">
    <board-component :board="board" :current-player="currentPlayer" :swap-player="swapPlayer" />
  </div>  

</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { Board } from '@/models/Board';
import BoardComponent from './components/BoardComponent.vue';
import { Player } from './models/Player';
import { Colors } from './models/Colors';

const board = ref();
const whitePlayer = ref<Player>(new Player(Colors.WHITE));
const blackPlayer = ref<Player>(new Player(Colors.BLACK));
const currentPlayer = ref<Player | null>(null);

function restart() {
  const newBoard = new Board();
  newBoard.initCells();
  newBoard.addFigures();
  board.value = newBoard;
}

function swapPlayer() {
  currentPlayer.value = currentPlayer.value?.color === Colors.WHITE ? blackPlayer.value : whitePlayer.value;
}

onMounted(() => {
  restart();
  currentPlayer.value = whitePlayer.value;
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
