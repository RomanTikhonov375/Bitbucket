<template>
    <main class="main">
        <MyHeader :options="options"></MyHeader>
        <section class="products" aria-label="страница с товарами">
            <MyForm @create="createCard"></MyForm>
            <transition name="fade">
                <MyPopup v-if="isProductAdd"></MyPopup>
            </transition>

            <CardsList :productCards="productCards" @remove="removeCard"></CardsList>

        </section>

    </main>
</template>

<script setup>
import MyHeader from '@/components/MyHeader.vue'
import MyForm from '@/components/MyForm.vue'
import CardsList from '@/components/CardsList.vue'
import MyPopup from '@/components/UI/MyPopup.vue';
import { onMounted, provide, ref, watch } from 'vue';

const parrentSelectedOption = ref({})
provide('parrentSelectedOption', parrentSelectedOption)

const productCards = ref([]);
let isProductAdd = ref(false);

const options = ref([
{
    value: 'title',
    name: 'По наименованию'

},
{
    value: 'price',
    name: `По цене ↑`
},
{
    value: 'price',
    name: 'По цене ↓'
}
])


const createCard = (card) => {
    isProductAdd.value = true
    productCards.value.push(card)
    setTimeout(() => {
        isProductAdd.value = false
    }, 1000)
    localStorage.setItem('cards', JSON.stringify(productCards.value))
}

const removeCard = (card) => {
    productCards.value = productCards.value.filter(p => p.id !== card.id)
    localStorage.setItem('cards', JSON.stringify(productCards.value))
}

watch(parrentSelectedOption, (newValue) => {
    
    productCards.value.sort((cardA, cardB) => {
        if (newValue.name === 'По наименованию') {
            return cardA[newValue.value]?.localeCompare(cardB[newValue.value])
        } else if (newValue.name === 'По цене ↓') {
            return cardA[newValue.value] - cardB[newValue.value]
        } else if (newValue.name === 'По цене ↑') {
            return cardB[newValue.value] - cardA[newValue.value]
        } else {
            return 
        }
        
    })
});

onMounted(() => {
    productCards.value = JSON.parse(localStorage.getItem('cards'))
})

</script>

<style lang="scss">
@use './variabels/variabels' as v;
@import '../vendor/normalize.css';


.main {
    padding: 32px;
    max-width: 1440px;
    box-sizing: border-box;
    background-color: v.$dark-white;
    display: flex;
    flex-direction: column;

}

.products {
    display: flex;
    gap: 16px;
    align-items: flex-start;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

@media screen and (max-width: 725px) {
    .products {
        flex-direction: column;
    }
}
</style>