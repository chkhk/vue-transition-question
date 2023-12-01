<template>
  <div id="random-choice" class="f-c-c">
    <textarea
      cols="30"
      rows="5"
      v-model="text"
      style="resize: vertical"
    ></textarea>
    <div class="box f-c">
      <div
        v-for="(i, index) in textArr"
        :key="index"
        ref="allStr"
        class="str-box"
      >
        {{ i }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';

const text = ref('');
const allStr = ref(null);

const textArr = computed(() => {
  if (text.value.match(/^\s*$/)) {
    return [];
  } else {
    return text.value.split(/[,，]/).filter((i) => !i.match(/^\s*$/));
  }
});

// 任意代码修改都可复现
// console.log(1);
</script>

<style scoped>
#random-choice {
  width: 100%;
  gap: 25px;
  position: absolute;
}
.box {
  gap: 10px;
  align-items: flex-start;
  flex-wrap: wrap;
}
.str-box {
  padding: 5px 10px;
  border-radius: 30px;
  border: 1px solid gray;
  color: white;
  background-color: gray;
}
.str-box.active {
  background-color: black;
}
</style>
