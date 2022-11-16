<template>
    <div class="card-back">
        <img src="../assets/images/bg-card-back.png" alt="Card back">
        <p class="cvc">{{cvc}}</p>
    </div>
</template>

<script setup>
    defineProps({
        cvc: String,
    })
</script>

<style lang="scss" scoped>

</style>