<template>
    <div>
        <h2>Curent player: {{ currentPlayer?.color }}</h2>
        <div class="board-wrap">
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
            <div class="board-nums" >
                <span class="board__num" v-for="num in [1,2,3,4,5,6,7,8]" :key="num">{{ num }}</span>
            </div>
        </div>
        <div class="board-letters" >
            <span class="board__letter" v-for="letter in ['A','B','C','D','E','F','G','H']" :key="letter">{{ letter }}</span>
        </div>
    </div>

</template>

<script setup lang="ts">
import { Board } from '@/models/Board';
import { defineProps, ref, watch } from 'vue';
import CellComponent from './CellComponent.vue';
import { Cell } from '@/models/Cell';
import { Player } from '@/models/Player';
interface Props {
    board?: Board;
    currentPlayer: Player | null;
    swapPlayer: () => void;
}

const props = defineProps<Props>();

const selectedCell = ref<Cell | null>(null);

const clickOnCell = (cell: Cell) => {
    if (selectedCell.value && selectedCell.value !== cell && selectedCell.value.figure?.canMove(cell)) {
        selectedCell.value.moveFigure(cell);
        selectedCell.value = null;
        props.swapPlayer();
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
    props.board?.highlightCells(selectedCell.value as Cell);
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

    &-wrap {
        display: flex;
    }

    &-nums {
        display: flex;
        justify-content: center;
        flex-direction: column-reverse;
    }

    &__num {
        height: 70px;
        display: flex;
        align-items: center;
    }

    &-letters {
        display: flex;
    }

    &__letter {
        width: 70px;
        display: flex;
        justify-content: center;
    }
  }
</style>