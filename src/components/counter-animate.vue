<template>
  <div class="counter">
    <div class="counter__show">
      <p class="counter__num" ref="numRef" :class="{ bounce: isAnimate }">{{ store.counter }}</p>
    </div>
    <div class="counter__operate">
      <div class="counter__button--group">
        <button class="btn" @click="changeCounter(1)">+</button>
        <button class="btn" @click="changeCounter(-1)">-</button>
      </div>
      <button class="btn coutner__reset" @click="reset">reset</button>
    </div>
  </div>
</template>
<script lang="ts" setup>
import { ref } from 'vue';
import { counterStore } from '@/store/counter';

const isAnimate = ref<boolean>(false);
const numRef = ref<HTMLElement | null>(null);
const store = counterStore();
const { changeCounter } = store;

store.$onAction(() => {
  isAnimate.value = true;
  // 动画结束移除bounce
  numRef.value?.addEventListener('animationend', () => {
    isAnimate.value = false;
  });
});

const reset = () => {
  store.$reset();
};
</script>
<style lang="scss" scoped>
.counter {
  &__show {
    height: 300px;
    background: #304acd;
    box-shadow: 0px 4px 16px 0px #6a80ef;
    display: flex;
    align-items: center;
  }
  &__num {
    width: 100%;
    color: #fff;
    font-weight: bold;
    font-size: 8rem;
    text-align: center;
  }
}
.btn {
  outline: 0;
  border: 1px solid rgb(49 74 204 / 30%);
  border-radius: 2px;
  background: rgb(49 74 204);
  min-width: 56px;
  min-height: 32px;
  color: #fff;
  cursor: pointer;
  &:active {
    background: rgb(49 74 204 / 80%);
  }
}
.counter__operate {
  margin-top: 20px;
  display: flex;
  justify-content: center;
}
.counter__button--group {
  .btn {
    &:active {
      background: rgb(49 74 204 / 80%);
    }
    &:first-child {
      border-right: 0;
      border-top-right-radius: 0;
      border-bottom-right-radius: 0;
    }
    &:last-child {
      border-left: 0;
      border-top-left-radius: 0;
      border-bottom-left-radius: 0;
    }
    &:not(:last-child):not(:first-child) {
      border-right: 0;
      border-left: 0;
      border-radius: 0;
    }
  }
}
.coutner__reset {
  margin-left: 10px;
}
.bounce {
  animation: bounceAni 0.3s both;
}

@keyframes bounceAni {
  from {
    transform: translateY(0);
  }
  60% {
    transform: translateY(-20px);
  }
  80% {
    transform: translateY(10px);
  }
  90% {
    transform: translateY(4px);
  }
  to {
    transform: translateY(0);
  }
}
</style>
