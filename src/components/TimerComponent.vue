<template>
    <div>
        <button @click="emits('restart')">Restart game</button>

    </div>
</template>

<script setup lang="ts">
import { Player } from '@/models/Player';
import { defineProps, defineEmits } from 'vue';

interface Props {
    currentPlayer: Player | null;
}
interface Emits {
  (e: 'restart'): void;
}

const props = defineProps<Props>();
const emits = defineEmits<Emits>()

</script>
<style lang="scss" scoped>
 
</style>