<template>
  <div id="random-choice" class="f-c-c">
    <h3>选项使用逗号隔开，按下回车开始随机选择</h3>
    <div class="text-box">
      <button @click="text = ''">重置</button>
      <button @click="randomStr">随机</button>
      <textarea
        cols="30"
        rows="5"
        v-model="text"
        @keydown.enter.prevent="randomStr"
      ></textarea>
    </div>
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
import { computed, onBeforeUnmount, ref, watch } from 'vue';

const text = ref('');
const allStr = ref(null);

let oldIndex = 0;
let intervalId;
let timeoutId;
function randomStr() {
  clearAll();
  if (allStr.value.length < 1) return;
  const arr = [...allStr.value];
  intervalId = window.setInterval(() => {
    if (arr.length === 1) {
      const list = arr[0].classList;
      if (list.contains('active')) {
        list.remove('active');
      } else {
        list.add('active');
      }
    } else {
      let index = getRadomIndex(arr.length - 1);
      arr[index].classList.add('active');
      arr[oldIndex].classList.remove('active');
      oldIndex = index;
    }
  }, 100);
  timeoutId = window.setTimeout(() => {
    window.clearInterval(intervalId);
  }, 2000);
}

function getRadomIndex(nub) {
  let index = randomNumber(0, nub);
  if (index === oldIndex) {
    index = getRadomIndex(nub);
  }
  return index;
}

function clearAll() {
  window.clearInterval(intervalId);
  window.clearTimeout(timeoutId);
  if (allStr.value && allStr.value.length > 0) {
    allStr.value[oldIndex]?.classList.remove('active');
  }
}

watch(text, () => {
  clearAll();
});

/** @type {ComputedRef<String[]>} */
const textArr = computed(() => {
  if (text.value.match(/^\s*$/)) {
    return [];
  } else {
    return text.value.split(/[,，]/).filter((i) => !i.match(/^\s*$/));
  }
});

onBeforeUnmount(() => {
  clearAll();
});

function randomNumber(min = 0, max = 1) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

console.log(1);
</script>

<style scoped>
#random-choice {
  width: 100%;
  padding: 30px 10px;
  gap: 25px;
  position: absolute;
}

.text-box {
  width: 500px;
  max-width: 100%;
}

button {
  float: right;
  font-size: x-small;
}
textarea {
  width: 100%;
  resize: vertical;
  box-shadow: 1px 1px 1px #999;
}
.box {
  gap: 10px;
  align-items: flex-start;
  flex-wrap: wrap;
}

.str-box {
  user-select: text;
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
