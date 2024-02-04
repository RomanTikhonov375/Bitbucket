<template>
    <li class="product-card">

        <img class="product-card__image" :src="props.card.imgUrl">
        <h2 class="product-card__title">{{ props.card.title }}</h2>
        <p class="product-card__description">{{ props.card.description }}</p>
        <p class="product-card__price">{{ props.card.price }} руб.</p>
    </li>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
    card: {
        type: Object
    }
})

</script>

<style lang="scss" scoped>
@use '../variabels/variabels' as v;

.product-card {
    display: flex;
    position: relative;
    flex-direction: column;
    gap: 16px;
    max-width: 332px;
    border-radius: 4px;
    background: v.$white08;
    cursor: pointer;
    overflow: hidden;
    transition: box-shadow 0.3s ease-out;
    box-shadow: 0px 6px 10px 0px rgba(0, 0, 0, 0.02), 0px 20px 30px 0px rgba(0, 0, 0, 0.04);

    &:hover .product-card__image {
        transform: scale(1.2);
    }

    &:hover {
        box-shadow: 0px 6px 10px 0px rgba(0, 0, 0, 0.08), 0px 20px 30px 0px rgba(0, 0, 0, 0.04);
    }
}

.product-card__image {
    object-fit: cover;
    width: 100%;
    transition: transform 0.3s ease-out;
    overflow: hidden;
}

.product-card__title {
    padding-top: 10px;
    overflow: hidden;
    margin: 0;
    @include v.H2;
    padding-left: 16px;
}

.product-card__description {
    @include v.P-normal;
    margin: 0;
    padding: 0 16px;
}

.product-card__price {
    @include v.P-big;
    padding-left: 16px;
    margin: 16px 0 24px 0;

}
</style>