<template>
    <form class="product-order-form">
        <ul class="product-order-form__inputs-wrapper">
            <MyInput v-model="card.title" for="product-name" type="text" placeholder="Введите наименование товара"></MyInput>
            <MyTextarea for="product-description" placeholder="Введите описание товара"></MyTextarea>
            <MyInput v-model="card.imgUrl" for="product-image-link" type="url" placeholder="Введите ссылку"></MyInput>
            <MyInput v-model="card.price"  for="product-price" type="numeric" placeholder="Введите цену"></MyInput>
            <MyButton type="submit" buttonText="Добавить товар"></MyButton>
        </ul>


    </form>
</template>

<script setup>
import MyInput from '@/components/UI/MyInput'
import MyTextarea from '@/components/UI/MyTextarea'
import MyButton from '@/components/UI/MyButton'

const card = {
    imgUrl: '',
    title: '',
    description: '',
    price: ''
}
</script>

<style lang="scss" scoped>
@use '../variabels/variabels' as v;

.product-order-form {
    display: flex;
    flex-direction: column;
    gap: 24px;
    padding: 24px;
    box-sizing: border-box;
    min-width: 332px;
    height: 440px;
    border: 0;
    background-color: v.$white08;
    box-shadow: 0px 6px 10px 0px rgba(0, 0, 0, 0.02), 0px 20px 30px 0px rgba(0, 0, 0, 0.04);
    flex-grow: 1;

}

.product-order-form__inputs-wrapper {
    display: flex;
    flex-direction: column;
    gap: 16px;
    border: 0;
    padding: 0;
    margin: 0;
    list-style: none;
}







@media screen and (max-width: 725px) {
    .product-order-form {
        width: 332px;
        align-self: center;
    }
}

@media screen and (max-width: 375px) {
    .product-order-form {
        min-width: 0;
        width: 100%;
    }
}
</style>