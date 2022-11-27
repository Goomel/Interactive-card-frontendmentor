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
        position: relative;
        width: 220px;
        transform: translateX(15%);
        &-img{
           width: 100%;
        }
        .cvc{
            position: absolute;
            top: 41%;
            right: 13%;
            // transform: translateY(50%);
            color: var(--light-grayish-violet);
            font-size: 12px;
            font-family: 'Manrope', sans-serif;
            font-weight: 500;
            z-index: 1;
        }
    }
    @media(min-width: 375px){
        .card-back{
            width: 280px;
        }
    }
    @media (min-width: 768px) {
        .card-back{
            width: 350px;
        }
    }
    @media(min-width: 992px){
        .card-back{
                transform: translate(10%, 0);
                margin-top: 1em;
                .cvc{
                    top: 43%;
                }
        }
    }

    
</style>