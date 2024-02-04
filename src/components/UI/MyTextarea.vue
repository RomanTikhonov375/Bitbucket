<template>
    <li class="product-order-form__input-wrapper">
        <label class="product-order-form__form__input-label" :for="attrs.for">Описание товара<div
                class="product-order-form__label-req"></div></label>
        <textarea :value="props.modelValue" class="product-order-form__input product-order-form__textarea" :id="attrs.for"
            :placeholder="attrs.placeholder" @input="updateInput"></textarea>
    </li>
</template>

<script >
export default {
    inheritAttrs: false
}
</script>

<script setup>


import { useAttrs, defineProps, defineEmits  } from 'vue'
const attrs = useAttrs();
const props = defineProps({
    modelValue: {   
        default: null
    },
})

const emit = defineEmits(['update:modelValue'])

function updateInput(event) {
    emit('update:modelValue', event.target.value)
            }
</script>

<style lang="scss" scoped>
.product-order-form__textarea {
    min-height: 108px;
    resize: none;
}
</style>