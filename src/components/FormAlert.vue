<template>
    <div class="form-alert">
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
        left: 0;
        z-index: 2;
        background-color: var(--white);
    }
</style>