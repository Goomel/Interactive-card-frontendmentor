<template>
    <div class="form-alert">
        <img src="../assets/images/icon-complete.svg" alt="Complete">
        <h2>Thank you!</h2>
        <p>We've added your card details</p>
        <ConfirmButton btn-text="Continue"/>
    </div>
</template>

<script setup>
    import ConfirmButton from './ConfirmButton.vue';
</script>

<style lang="scss" scoped>
    .form-alert{
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 50%;
        padding: 0 5%;
        transform: translateX(-50%);
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        z-index: 2;
        background-color: var(--white);
    }
</style>