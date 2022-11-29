<template>
    <div class="form-alert">
        <img src="../assets/images/icon-complete.svg" alt="Complete">
        <h2 class="form-alert__thanks">Thank you!</h2>
        <p class="form-alert__info">We've added your card details</p>
        <ConfirmButton btn-text="Continue" @submit="props.closeFormAlert"/>
    </div>
</template>

<script setup>
    import ConfirmButton from './ConfirmButton.vue';
    const props = defineProps({
        closeFormAlert: Function
    })
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
        &__thanks{
            text-transform: uppercase;
            color: var(--very-dark-violet);
            font-weight: 400;
            letter-spacing: 3px;
            margin: .8em 0;
        }
        &__info{
            color: var(--dark-grayish-violet);
            margin-bottom: 2em;
        }
    }
    @media(min-width: 992px){
        .form-alert{
            left: 60%;
            width: 55%;
        }
    }
</style>