<script setup lang="ts">
import { reactive } from "vue";
// let answer = "";
const state = reactive({ message: "", currentQuestion: 0,answer:"" });
let exams = [
  { question: "「我」的注音是哪個", answer: "ㄨㄛˇ", options: ["ㄛˇ", "ㄨㄛˇ", "ㄊㄚ", "ㄋ一ˇ"] },
  { question: "古稀之年是幾歲:", answer: "70", options: ["70", "90", "60", "80"] },
  { question: "狀元是第幾名:", answer: "一", options: ["一", "二", "三", "四"],
  },
  { question: "不惑之年是幾歲:", answer: "40", options: ["20", "30", "40", "50"],},
  { question: "鴨子怎麼叫:", answer: "呱", options: ["呱", "咩", "哞", "汪"], },
];
function generateQuestion() {
  if (exams[state.currentQuestion].answer === state.answer) {
    state.message = "答案正確";
    if (state.currentQuestion + 1 < exams.length) {
      state.currentQuestion++;
    }
  } else {
    state.message = "答案錯誤";
  }

}
</script>
<template>
  <div>
    {{ exams[state.currentQuestion].question }}
    <span v-for="option in exams[state.currentQuestion].options" :key="option" >
    <input type="radio" v-model="state.answer" :value="option" />
    {{ option }}
  </span>
    {{ state.message }}
    <button @click="generateQuestion">下一題</button>
  </div>

</template>