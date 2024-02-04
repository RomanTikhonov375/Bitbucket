<template>
    <ul class="products-list">
        <ProductCard v-for="card in props.productCards" :card="card" :key="card.id"></ProductCard>
    </ul>
</template>

<script setup>
import ProductCard from '@/components/ProductCard.vue'
import { defineProps } from 'vue'
const props = defineProps({
    productCards: {
        type: Array,
    }
})

</script>

<style lang="scss" scoped>
    .products-list {
        margin: 0;
        padding: 0;
        list-style: none;
        display: flex;
        gap: 16px;
        flex-wrap: wrap;
        justify-content: center;
        box-sizing: border-box;
    }

    @media screen and (max-width: 375px) {
    .products-list {
        width: 100%;
        flex-direction: column;
        align-items: center;
    }
}
</style>