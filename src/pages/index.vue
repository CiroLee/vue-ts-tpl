<template>
  <div class="home">
    <counter-animate />
    <div class="home__other">
      <a href="https://github.com/CiroLee/mew-cli" target="_blank">more info about mew-cli</a>
    </div>
  </div>
</template>
<script lang="ts" setup>
import counterAnimate from '@/components/counter-animate.vue';
</script>
<style lang="scss" scoped>
.home {
  &__other {
    margin-top: 10%;
    text-align: center;
    font-size: 14px;
  }
}
</style>
