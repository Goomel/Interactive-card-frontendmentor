<template>
    <div class="card-back">
        <img src="../assets/images/bg-card-back.png" alt="Card back" class="card-back-img">
        <p class="cvc">{{cvc}}</p>
    </div>
</template>

<script setup>
    defineProps({
        cvc: String,
    })
</script>

<style lang="scss" scoped>
    .card-back{
        width: fit-content;
        width: 280px;
        &-img{
           width: 100%;
        }
        
    }
</style>