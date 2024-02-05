<template>
    <ul class="products-list">
        <transition-group name="list">
            <ProductCard class="list-item" v-for="card in props.productCards" :card="card" :key="card.id"
                @remove="emit('remove', card)"></ProductCard>
        </transition-group>
    </ul>
</template>

<script setup>
import ProductCard from '@/components/ProductCard.vue'
import { defineProps, defineEmits } from 'vue'
const props = defineProps({
    productCards: {
        type: Array,

    }
})

const emit = defineEmits('remove')

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

.list-item {
    transition: all 0.8s ease;
    display: inline-block;
    margin-right: 10px;
}

.list-enter-active,
.list-leave-active {
    transition: all 1s ease;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateY(30px);
}

@media screen and (max-width: 410px) {
    .products-list {
        width: 100%;
        flex-direction: column;
        align-items: center;
    }
}
</style>