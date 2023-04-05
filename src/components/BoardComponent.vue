<template>
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
</template>

<script setup lang="ts">
import type { Board } from '@/models/Board';
import { defineProps, defineEmits, ref, watch } from 'vue';
import CellComponent from './CellComponent.vue';
import type { Cell } from '@/models/Cell';
interface Props {
    board: Board;
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
    } else {
        selectedCell.value = cell;
    }
    if (!cell.figure) {
        selectedCell.value = null;
        return;
    }
}
const highlightCells = () => {
    props.board.highlightCells(selectedCell.value);
}

const updateBoard = () => {
    emit('update-board', props.board.getCopyBoard())
}

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