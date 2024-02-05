<template>
    <div class="center popup">
        <div class="popup__icon">
        </div>
        <div class="popup__title">
            Товар успешно добавлен!
        </div>

    </div>
</template>

<script setup>

</script>

<style scoped lang="scss">
.center {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);

}

.popup {
    z-index: 10;
    width: 350px;
    height: 200px;
    padding: 30px 20px;
    background-color: white;
    border-radius: 10px;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 1px solid grey;
}

.popup__icon {
    background-image: url('../../images/popup-icon.svg');
    background-repeat: no-repeat;
    width: 100px;
    height: 100px;
}
</style>