<script setup lang="ts">
import Hero from './components/Hero.vue';
import SigninForm from './components/SigninForm.vue';
</script>

<template>
  <div class="container">
    <div class="left"><Hero /></div>
    <div class="right"><SigninForm /></div>
  </div>
</template>

<style lang="scss" scoped>
  .container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    justify-self: center;
    
    .left {
      background-color: var(--color-secondary);
      border-radius: 0 20px 20px 0;
    }
  }

  @media screen and (width < 1024px) {
    .container {
      display: flex;
      flex-direction: column;
      align-items: center;

      .left {
        background-color: var(--color-white);
        border-radius: 0;
      }
    }
  }
</style>
