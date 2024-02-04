<template>
    <form class="product-order-form" @submit.prevent="handleSubmit(card)">
        <ul class="product-order-form__inputs-wrapper">
            <MyInput v-model="card.title" for="product-name" type="text" placeholder="Введите наименование товара">
                Наименование товара</MyInput>
            <span class="product-order-form__input-error" v-for="error in v$.title.$errors" :key="error.$uid">{{
                error.$message }}</span>
            <MyTextarea v-model="card.description" for="product-description" placeholder="Введите описание товара">Описание
                товара</MyTextarea>
            <span class="product-order-form__input-error" v-for="error in v$.description.$errors" :key="error.$uid">{{
                error.$message }}</span>
            <MyInput v-model="card.imgUrl" for="product-image-link" type="text" placeholder="Введите ссылку">Ссылка на
                изображение товара</MyInput>
            <span class="product-order-form__input-error" v-for="error in v$.imgUrl.$errors" :key="error.$uid">{{
                error.$message }}</span>
            <MyInput v-model="card.price" for="product-price" type="numeric" placeholder="Введите цену">Цена товара
            </MyInput>
            <span class="product-order-form__input-error" v-for="error in v$.price.$errors" :key="error.$uid">{{
                error.$message }}</span>
            <MyButton :disabled="(v$.$invalid)" type="submit" buttonText="Добавить товар"></MyButton>
        </ul>


    </form>
</template>

<script setup>
import { useVuelidate, } from '@vuelidate/core'
import { required, url, } from '@vuelidate/validators'
import MyInput from '@/components/UI/MyInput'
import MyTextarea from '@/components/UI/MyTextarea'
import MyButton from '@/components/UI/MyButton'
import { reactive, defineEmits } from 'vue'

let card = reactive({
    imgUrl: '',
    title: '',
    description: '',
    price: ''
})

const rules = {
    title: { required },
    description: { required },
    imgUrl: { required, url },
    price: {
        required,
    }
}

const emit = defineEmits(['create'])

const v$ = useVuelidate(rules, card)

const handleSubmit = async (card) => {
    const result = await v$.value.$validate()
    if (result) {
        card.id = Date.now();
        emit('create', card);
        card = {
            imgUrl: '',
            title: '',
            description: '',
            price: ''
        }
    } else {
        alert('Что то пошло не так')
    }
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
    min-height: 440px;
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

.product-order-form__input-error {
    @include v.P-small-3;
    color: red;
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
}</style>