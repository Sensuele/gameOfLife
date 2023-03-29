<template>
    <div :class="cell.color" class="cell">
        <img v-if="cell.figure?.logo" :src="cell.figure.logo" alt="">
    </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';
import type { Cell } from '@/models/Cell';
interface Props {
    cell: Cell;
}
// interface Emits {
//   (e: 'unlink'): void;
// }

const props = defineProps<Props>();
// const emit = defineEmits<Emits>();
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
</style>