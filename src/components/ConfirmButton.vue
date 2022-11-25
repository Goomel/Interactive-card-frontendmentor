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
      margin-top: 20px;
      font-size: 18px;
      background-color: var(--very-dark-violet);
      color: var(--light-grayish-violet);
      border: 0px;
      border-radius: 10px;
   }
</style>