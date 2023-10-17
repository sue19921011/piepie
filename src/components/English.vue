<script setup lang="ts">
import { reactive } from "vue";
let answer = "";
const state = reactive({ message: "", currentQuestion: 0,answer:[] });
let exams = [
      { question: "蔬菜水果的英文", answer: ["fruit", "vegetable"], options: ["fruit", "vegetable","cow","loud"] },
      { question: "哪些英文是母音", answer: ["a", "u"], options: ["a", "u", "p", "n"] },
      { question: "牛是哪三個英文字母", answer: ["c", "o", "w"], options: ["a", "c", "o", "w"] },
      { question: "螞蟻是哪三個英文字母", answer: ["a", "n", "t"], options: ["a", "n", "t", "c"] },
      { question: "滑鼠是哪個開頭哪個結尾", answer: ["m", "e",], options: ["m", "e", "p", "l"] }
    ];

    function generateQuestion() {
  if (exams[state.currentQuestion].answer.length === state.answer.length) {
    let correct = 0;
    for (var item of state.answer) {
      if (exams[state.currentQuestion].answer.includes(item)) {
        correct++;
      }
    }
    if (correct == exams[state.currentQuestion].answer.length) {
      state.message = "答案正確";
      if (state.currentQuestion + 1 < exams.length) {
        state.currentQuestion++;
        state.answer = []; //清空上次的答案，否則會讀到上次的值
      }
    } else {
      state.message = "答案錯誤";
    }
  } else {
    state.message = "答案錯誤";
  }
}
</script>
<template>
  <div>
    {{ exams[state.currentQuestion].question }}
    <span v-for="option in exams[state.currentQuestion].options">
    <input type="checkbox" v-model="state.answer" :value="option" />
    {{ option }}
  </span>
    {{ state.message }}
    <button @click="generateQuestion">下一題</button>
  </div>

</template>