<template>
    <div class="card-front">
        <img src="../assets/images/bg-card-front.png" alt="Card front">
        <p class="card-name">{{cardholderName}}</p>
        <p class="card-number">{{cardNumber}}</p>
        <p class="expiration-date">
            <span class="month">{{month}}</span>
            <span class="year">{{year}}</span>
        </p>
    </div>
</template>

<script setup>
    defineProps({
        cardholderName: String,
        cardNumber: String,
        month: String,
        year:String,
    })
</script>

<style lang="scss" scoped>

</style>