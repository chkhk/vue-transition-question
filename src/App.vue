<template>
  <h3>
    在文本框中输入内容，然后修改组件内容后回到浏览器，查看组件所在的 dom
    结构，可以发现重复渲染
  </h3>
  <button @click="show = !show">{{ show ? 'hide' : 'show' }}</button>
  <div id="app2" class="f-c">
    <transition
      enter-active-class="animate__animated animate__slideInLeft"
      leave-active-class="animate__animated animate__fadeOutRight"
    >
      <component
        v-if="show"
        :key="Math.random()"
        :is="HelloWorld"
        @vue:mounted="childrenMounted"
      />
    </transition>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue';

const show = ref(true);

function childrenMounted() {
  console.log('childrenMounted');
}
</script>

<style>
button {
  font-size: xx-large;
}
#app2 {
  width: 100vw;
  height: 50vh;
  align-items: flex-start;
  position: absolute;
}
</style>
