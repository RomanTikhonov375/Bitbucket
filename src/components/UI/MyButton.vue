<template>
    <button :type="attrs.type" class="product-order-form__sbm-button">{{ attrs.buttonText }}</button>
</template>

<script>
export default {
    inheritAttrs: false
}
</script>

<script setup>
import { useAttrs } from 'vue'
const attrs = useAttrs();
</script>

<style lang="scss" scoped>
@use '../../variabels/variabels' as v;
.product-order-form__sbm-button {
    cursor: pointer;
    border: 0;
    background-color: v.$grey200;
    @include v.P-small-2;
    padding: 10px;
    border-radius: 10px;
    transition: opacity 0.3s ease-in;

    &:hover {
        opacity: 0.8;
    }

    &:focus-visible {
        outline: 1px solid grey;
    }

    &:active {
        outline: 1px solid grey;
    }

    &:focus {
        outline: 1px solid rgb(227, 221, 194);
    }
}</style>