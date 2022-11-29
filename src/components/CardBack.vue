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
            top: 38%;
            right: 13%;
            color: var(--light-grayish-violet);
            font-size: 16px;
            font-family: 'Manrope', sans-serif;
            font-weight: 800;
            z-index: 1;
        }
    }
    @media(min-width: 375px){
        .card-back{
            width: 280px;
            .cvc{
                top: 40%;
                font-size: 18px;
            }
        }
    }
    @media (min-width: 768px) {
        .card-back{
            width: 350px;
            .cvc{
                top: 42%;
            }
        }
    }
    @media(min-width: 992px){
        .card-back{
                width: 380px;
                transform: translate(10%, 0);
                margin-top: 1em;
        }
    }
    @media(min-width: 1200px){
        .card-back{
            width: 450px;
            .cvc{
                top: 43%;
            }
        }
    }
    
</style>