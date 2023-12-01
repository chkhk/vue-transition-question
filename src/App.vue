<template>
  <h3 style="margin-bottom: 50px">
    在文本框中输入内容，然后修改组件内容后回到浏览器，查看组件所在的 dom
    结构，可以发现有多个一模一样的组件
  </h3>
  <hr />
  <transition
    enter-active-class="animate__animated animate__slideInLeft"
    leave-active-class="animate__animated animate__fadeOutRight"
  >
    <HelloWorld v-if="show"></HelloWorld>
  </transition>
</template>

<script setup>
import { ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue';

const show = ref(true);

/* eslint-disable */
function childrenMounted() {
  console.log('childrenMounted');
}
</script>
