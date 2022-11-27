<template>
   <button type="submit" class="confirm-btn" @click.prevent="$emit('submit')">{{props.btnText}}</button>
</template>

<script setup>
   const props = defineProps({
      btnText: {
         type: String,
         default: "Confirm"
      }
   })
</script>

<style lang="scss" scoped>
   .confirm-btn {
      width: 100%;
      padding: 20px 0;
      margin: 1.5em 0;
      font-size: 14px;
      background-color: var(--very-dark-violet);
      color: var(--light-grayish-violet);
      border: 0px;
      border-radius: 10px;
      cursor: pointer;
   }
   @media (min-width:992px){
      .confirm-btn{
         padding: 15px 0;
         margin: 1em 0;
      }
   }
</style>