<template>
    <div class="section__header-wrapper">
        <h1 class="section__header-title">Добавление товара</h1>
        <select class="select" aria-placeholder="Сортировка списка">
            <option  class="select__option">По умолчанию</option>
            <option  class="select__option">По возростанию цену</option>
            <option  class="select__option">По убыванию цены</option>
            <option  class="select__option">По наименовани</option>
        </select>
    </div>
</template>

<script>

</script>

<style lang="scss" scoped>
@use '../variabels/variabels' as v;

.section__header-wrapper {
    display: flex;
    justify-content: space-between;
    margin-bottom: 16px;

}

@media screen and (max-width: 450px) {
        .section__header-wrapper {
            flex-direction: column;
            gap: 10px;
            align-items: center
        }
    }

.section__header-title {
    @include v.H1;
    margin: 0;
}

.select {
    padding: 10px 0 10px 16px;
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
</style>