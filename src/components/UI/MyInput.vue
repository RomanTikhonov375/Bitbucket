<template >
    <li class="product-order-form__input-wrapper">
        <label class="product-order-form__form__input-label" :for="attrs.for"><slot></slot><div
                class="product-order-form__label-req"></div></label>
        <input :type="attrs.type" class="product-order-form__input" :id="attrs.for" :placeholder="attrs.placeholder"
             :value="props.modelValue" @input="updateInput">
    </li>
</template>

<script>
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
    v: {
        type: Object
    }
})

const emit = defineEmits(['update:model-value'])

function updateInput(event) {
    emit('update:model-value', event.target.value)
    props.v.$validate()
            }

</script>

<style lang="scss">
@use '../../variabels/variabels' as v;


.product-order-form__input-wrapper {
    display: flex;
    flex-direction: column;
    gap: 4px;
}

.product-order-form__form__input-label {

    @include v.P-small-3;
    color: v.$temp-darks-lesser;
    flex-shrink: 0;
    display: flex;
}

.product-order-form__label-req {
    width: 4px;
    height: 4px;
    border-radius: 4px;
    background: v.$pink;
}

.product-order-form__input {
    background-color: v.$dark-white;
    border-radius: 4px;
    border: 0;
    box-shadow: 0px 6px 10px 0px rgba(0, 0, 0, 0.02), 0px 20px 30px 0px rgba(0, 0, 0, 0.04);
    padding: 10px 0 11px 16px;
    @include v.P-small-2;
    transition: box-shadow 0.3s ease-in;

    &:hover {
        box-shadow: 0px 6px 10px 0px rgba(0, 0, 0, 0.08), 0px 20px 30px 0px rgba(0, 0, 0, 0.04);
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
}

</style>