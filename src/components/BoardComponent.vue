<template>
    <div class="board">
        <template v-for="(row) in board?.cells">
            <template v-for="(cell, index) in row" :key="index">
                <cell-component :cell="cell" />
            </template>
        </template>
    </div>
</template>

<script setup lang="ts">
import type { Board } from '@/models/Board';
import { defineProps, defineEmits } from 'vue';
import CellComponent from './CellComponent.vue';
interface Props {
    board: Board;
}
// interface Emits {
//   (e: 'unlink'): void;
// }

const props = defineProps<Props>();
// const emit = defineEmits<Emits>();
</script>

<style lang="scss" scoped>
  .board {
    width: calc(70px * 8);
    height: calc(70px * 8);
    display: flex;
    flex-wrap: wrap;
  }
</style>