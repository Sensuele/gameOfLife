<template>
    <div>
        <h2>Curent player: {{ currentPlayer?.color }}</h2>
        <div class="board">
            <template v-for="(row) in board?.cells">
                <template v-for="(cell, index) in row" :key="index">
                    <cell-component 
                        :cell="cell" 
                        :selected="selectedCell?.x === cell.x && selectedCell?.y === cell.y " 
                        @click-on-cell="clickOnCell"
                        />
                </template>
            </template>
        </div>
    </div>

</template>

<script setup lang="ts">
import { Board } from '@/models/Board';
import { defineProps, defineEmits, ref, watch } from 'vue';
import CellComponent from './CellComponent.vue';
import { Cell } from '@/models/Cell';
import { Player } from '@/models/Player';
interface Props {
    board: Board;
    currentPlayer: Player | null;
    swapPlayer: () => void;
}
interface Emits {
  (e: 'update-board', board: Board): void;
}

const props = defineProps<Props>();
const emit = defineEmits<Emits>();

const selectedCell = ref<Cell | null>(null);

const clickOnCell = (cell: Cell) => {
    if (selectedCell.value && selectedCell.value !== cell && selectedCell.value.figure?.canMove(cell)) {
        selectedCell.value.moveFigure(cell);
        selectedCell.value = null;
        props.swapPlayer();
        // updateBoard();
        console.log(props.board)
    } else {
        if (cell.figure?.color === props.currentPlayer?.color) {
            selectedCell.value = cell;

        }
    }
    if (!cell.figure) {
        selectedCell.value = null;
        return;
    }
}
const highlightCells = () => {
    props.board.highlightCells(selectedCell.value as Cell);
}

// const updateBoard = () => {
//     console.log(props.board)
//     emit('update-board', props.board.getCopyBoard())
// }

watch(selectedCell, () => {
    highlightCells();
})
</script>

<style lang="scss" scoped>
  .board {
    width: calc(70px * 8);
    height: calc(70px * 8);
    display: flex;
    flex-wrap: wrap;
  }
</style>