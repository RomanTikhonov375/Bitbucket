<template>
    <li class="product-card">

        <img class="product-card__image" :src="props.card.imgUrl">
        <h2 class="product-card__title">{{ props.card.title }}</h2>
        <p class="product-card__description">{{ props.card.description }}</p>
        <p class="product-card__price">{{ props.card.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ") }} руб.</p>
        <button class="product-card__trash" @click="emit('remove' , props.card)">Удалить</button>
    </li>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
    card: {
        type: Object
    }
})

const emit = defineEmits('remove')

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
    transition: box-shadow 0.3s ease-out;
    box-shadow: 0px 6px 10px 0px rgba(0, 0, 0, 0.02), 0px 20px 30px 0px rgba(0, 0, 0, 0.04);

    &:hover {
        box-shadow: 0px 6px 10px 0px rgba(0, 0, 0, 0.08), 0px 20px 30px 0px rgba(0, 0, 0, 0.04);
    }
}

.product-card__image {
    object-fit: cover;
    width: 332px;
    transition: transform 0.3s ease-out;
    height: 200px;

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

.product-card__trash {
    position: absolute;
    width: 24px;
    height: 24px;
    border: 0;
    border-radius: 20px;
    background-color: v.$pink;
    background-image: url('../images/trash.svg');
    background-repeat: no-repeat;
    background-position: center;
    font-size: 0;
    top:-12px;
    right: -12px;
    cursor: pointer;
}

@media screen and (max-width: 410px) {
    .product-card__image {
        width: 100%;
    }
    .product-card {
        width: 100%;
    }
}
</style>