<template>
    <section class="interactive-card">
        <div class="cards">
            <CardBack :cvc="cvc"/>
            <CardFront :cardholder-name="cardholderName" :card-number="cardNumber" :month="month" :year="year"/>
        </div>
        <div class="form-side">
            <form>
                <label>
                    Cardholder name
                    <input type="text" v-model="cardholderName" placeholder="e.g. Jane Appleseed">
                </label>
                <label>
                    Card number
                    <input type="text" v-model="cardNumber" placeholder="e.g. 1234 5678 9123 0000">
                </label>
                <label>
                    Exp. date (mm/yy)
                    <input type="text" v-model="month" placeholder="MM">
                    <input type="text" v-model="year" placeholder="YY">
                </label>
                <label>
                    CVC
                    <input type="text" v-model="cvc" placeholder="e.g. 123">
                </label>
                <ConfirmButton/>
            </form>
        </div>
    </section>

</template>

<script setup>
    import { ref } from 'vue';
    import CardFront from './CardFront.vue';
    import CardBack from './CardBack.vue';
    import ConfirmButton from './ConfirmButton.vue'

    const cardholderName = ref(null);
    const cardNumber = ref(null);
    const month = ref(null);
    const year = ref(null);
    const cvc = ref(null);
</script>   

<style lang="scss" scoped>

</style>