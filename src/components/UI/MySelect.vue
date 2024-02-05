<template>
    <div class="dropdown" ref="dropDown" @click="isDropDownVisible = !isDropDownVisible">
        <div class="dropdown__text">{{ props.modelValue.name || 'По умолчанию' }}<div class="dropdown__text-arrow"></div></div>
        <Transition name="slide-fade">
            <div class="dropdown__options-wrapper" v-if="isDropDownVisible">
                <div class="dropdown__option"
                    v-for="(option, index) in props.options" :key="index" @click="toggleOptionSelect(option)">
                    <p class="dropdown__option-text">{{ option.name || option }}</p>
                </div>
            </div>
        </Transition>


    </div>
</template>

<script setup>
import { defineProps, ref, defineEmits, onMounted, onBeforeUnmount } from 'vue';

const props = defineProps({
    options: {
        type: Array,
        reqired: true,
    },
    modelValue: {
        default: null
    }
})

const selecredOption = ref(null)
const dropDown = ref(null)
const emit = defineEmits(['update:modelValue'])


const toggleOptionSelect = (option) => {
        selecredOption.value = option
        emit('update:modelValue', option)
}

const isDropDownVisible = ref(false)

const onCloseDropDown = (element) => {
    if (!dropDown.value.contains(element.target)) {
        isDropDownVisible.value = false

    }
}

onMounted(() => {
    window.addEventListener('click', onCloseDropDown)
})

onBeforeUnmount(() => {
    window.removeEventListener('click', onCloseDropDown)
})


</script>

<style lang="scss" scoped>

@use '../../variabels/variabels' as v;
.dropdown {
    position: relative;
    padding: 10px 16px 10px 16px;
    border-radius: 4px;
    @include v.P-small-2;
    text-align: left;
    box-shadow: 0px 2px 5px 0px rgba(0, 0, 0, 0.10);
    border: 0;
    width: 122px;
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

.dropdown__button {
    width: 100%;
    height: 100%;
}

.dropdown__options-wrapper {
    z-index: 10;
    top: 32px;
    left: 0px;
    position: absolute;
    display: flex;
    width: 100%;
    padding: 2px 0px;
    flex-direction: column;
    align-items: flex-start;
    gap: 1px;
    border-radius: 2px;
    background: v.$white08;
}

.dropdown__option {
    display: flex;
    width: 100%;
    padding: 6px 12px;
    justify-content: center;
    align-items: flex-start;
    gap: 10px;
    align-self: flex-start;
    background: v.$white08;
    box-sizing: border-box;
    overflow: hidden;
    color: v.$grey900;
    text-overflow: ellipsis;
    white-space: nowrap;

    font-family: "Gotham Pro";
    font-size: 14px;
    font-style: normal;
    font-weight: 400;
    line-height: 20px;
    letter-spacing: 0.252px;
    cursor: pointer;
}

.dropdown__text {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.dropdown__option-text {
    width: 100%;
}

.dropdown__text-arrow {
    width: 4.59px;
    height: 4.59px;
    border-left: 1px solid v.$grey500;
    border-top: 1px solid v.$grey500;
    transform: rotate(225deg);
}

.dropdown__option-disabled {
    color: var(--gradients-grey, #868F98);
    opacity: 0.5;
    cursor: auto;
}

.dropdown__option:hover {
    background: v.$grey500;

}

.slide-fade-enter-active {
    transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
    transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
    transform: translateX(20px);
    opacity: 0;
}
</style>