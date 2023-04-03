<template>
    <div :class="[cell.color, selected ? 'selected' : '', cell.available && cell.figure ? 'available-attack' : '']" class="cell" @click="emit('clickOnCell', cell)">
        <div v-if="!cell.figure && cell.available" class="available"></div>
        <img v-if="cell.figure?.logo" :src="cell.figure.logo" alt="">
    </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';
import type { Cell } from '@/models/Cell';
interface Props {
    cell: Cell;
    selected: boolean;
}
interface Emits {
  (e: 'clickOnCell', cell: Cell): void;
}

const props = defineProps<Props>();
const emit = defineEmits<Emits>();
</script>

<style lang="scss" scoped>
.cell {
    width: 70px;
    height: 70px;
    display: flex;
    justify-content: center;
    align-items: center;

    img {
        width: 50px;
        height: 50px;
        position: relative;
    }
  }
.black {
background: deepskyblue;
}

.white {
background: #eed4ac;
}

.selected {
    background: brown;
}

.available {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: #22c022;
}

.available-attack {
    background: green;
}
</style>