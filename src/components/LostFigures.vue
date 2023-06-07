<template>
    <div class="lost">
        <h3>{{ title }}</h3>
        <template v-if="figures">
            <div v-for="figure in figures" :key="figure.id">
            {{ figure.name }}
            <div v-if="figure.logo">
                <img :src="figure.logo" alt="">
            </div>
            </div>
        </template>
    </div>
</template>

<script setup lang="ts">
import { Figure } from '@/models/figures/Figure';
import { defineProps} from 'vue';

interface Props {
    title: string;
    figures?: Figure[]
}

const props = defineProps<Props>();
</script>
<style lang="scss" scoped>
    .lost {
        height: calc(50vh - 60px);
        padding: 30px;
        margin-left: 50px;
        margin-right: 50px;
        background: lightgray;
        border-radius: 12px;
    }

    img {
        width: 20px;
        height: 20px;
    }
</style>
