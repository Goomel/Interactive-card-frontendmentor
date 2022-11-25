<template>
    <div class="card-front">
        <img src="../assets/images/bg-card-front.png" class="card-front-img" alt="Card front">
        <p class="card-name">{{props.cardholderName}}</p>
        <p class="card-number">{{formattedCardNumber}}</p>
        <p class="expiration-date">
            <span class="month">{{props.month}}</span>
            <span class="year">{{props.year}}</span>
        </p>
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
    /**
    * TODO: When you delete something from input, formattedCardNumber still gets it, FIX IT!
    * TODO: When cardNumber input is empty, formattedCardNumber gets 'undefined'
     */
    const formattedCardNumber = ref('');
    watch(cardNumber, (newCardNumber) => {
        formattedCardNumber.value += newCardNumber[newCardNumber.length-1]
        if(newCardNumber.length % 4 === 0 ){
            formattedCardNumber.value += ' '
        }
    })
</script>

<style lang="scss" scoped>
    .card-front{
        width: 280px;
        transform: translateY(-45%);
        &-img{
            width: 100%;
            max-width: 350px;
        }
        .card-number{
            color: white;
        }
    }
</style>