<template>
    <main class="main">
        <MyHeader></MyHeader>
        <section class="products" aria-label="страница с товарами">
            <MyForm :model="productCards" @create="createCard"></MyForm>
            <CardsList :productCards="productCards"></CardsList>
            
        </section>
       
    </main>
</template>

<script setup>
import MyHeader from '@/components/MyHeader.vue'
import MyForm from '@/components/MyForm.vue'
import CardsList from '@/components/CardsList.vue'

const productCards = []

const createCard = (card) => {
    productCards.push(card)
}

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

@media screen and (max-width: 725px) {
    .products {
        flex-direction: column;
}
    }
   

</style>