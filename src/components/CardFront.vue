<template>
    <div class="card-front">
        <img src="../assets/images/bg-card-front.png" class="card-front__img" alt="Card front">
        <img src="../assets/images/card-logo.svg" class="card-front__logo" alt="logo">
        <p class="card-name">{{props.cardholderName}}</p>
        <p class="card-number">{{formattedCardNumber}}</p>
        <p v-if="props.month" class="expiration-date">{{formattedExpDate}}</p>
    </div>
</template>

<script setup>
    import { ref, computed, watch } from 'vue';
    const props = defineProps({
        cardholderName: String,
        cardNumber: String,
        month: String,
        year: String,
    })

    const cardNumber = computed(()=>{
        return props.cardNumber
    })
    const formattedExpDate = computed(()=>{
        if(props.month.length < 2) return `0${props.month}/${props.year.slice(-2)}`;
        return `${props.month}/${props.year}`;
    })
    const formattedCardNumber = ref('');
    watch(cardNumber, (newCardNumber, oldCardNumber) => {
        const reg = /^\d+$/;
        if(newCardNumber.length === 0) formattedCardNumber.value = '';
        if(!reg.test(newCardNumber[newCardNumber.length-1])) return;
        if(newCardNumber.length >= oldCardNumber.length){
            formattedCardNumber.value += newCardNumber[newCardNumber.length-1]
            if(newCardNumber.length % 4 === 0 ){
                formattedCardNumber.value += ' '
            }
        }else{
            if(formattedCardNumber.value.charAt(formattedCardNumber.value.length-2) === ' ' || formattedCardNumber.value.charAt(formattedCardNumber.value.length-1) === ' '){
                formattedCardNumber.value = formattedCardNumber.value.slice(0,-2);
            }else{
                formattedCardNumber.value = formattedCardNumber.value.slice(0,-1);
            }
        }
    })
</script>

<style lang="scss" scoped>
    .card-front{
        position: relative;
        left: 5%;
        width: 220px;
        transform: translate(-15%, -45%);
        color: var(--light-grayish-violet);
        font-weight: 800;
        letter-spacing: 1.5px;
        &__img{
            width: 100%;
            z-index: 0;
        }
        &__logo{
            width: 50px;
            position: absolute;
            top: 0;
            left: 0;
            margin: 1em;
        }
        .card-name, .card-number, .expiration-date{
            position: absolute;
        }
        .card-number{
            top: 45%;
            left: 5%;
            font-size: 14px;
        }
        .card-name, .expiration-date{
            top: 70%;
            font-size: 12px;
        }
        .expiration-date{
            right: 5%;
        }
        .card-name{
            left: 5%;
            text-transform: uppercase;
            letter-spacing: 2px;
        }
    }
    @media(min-width: 375px){
        .card-front{
            width: 280px;
            .card-number{
                font-size: 20px;
            }
        }
    }
    @media (min-width: 768px) {
        .card-front{
            width: 350px;
            &__logo{
                width: 70px;
                margin: 1.3em;
            }
            .card-number{
                font-size: 24px;
            }
        }
    }
    @media(min-width: 992px){
        .card-front{
                width: 380px;
                transform: translate(-10%, 0);
                margin-bottom: 1em;
                .card-number{
                    font-size: 26px;
                    letter-spacing: 2px;
                }
            }
    }
    @media(min-width: 1200px){
        .card-front{
            width: 450px;
            .card-number{
                font-size: 28px;
            }
        }
    }
</style>