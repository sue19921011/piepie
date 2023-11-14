<script setup lang="ts">
import { ref, onMounted, watch } from 'vue';
import { getFirestore, collection, getDocs, query, where } from 'firebase/firestore';
import app from "@/components/settings/FirebaseConfig.vue";

const questions = ref([]);
const selectedOptions = ref([]);
const answerMessages = ref([]);
const selectedChapter = ref(null);

onMounted(created);

watch(selectedChapter, created);

async function created() {
  try {
    const db = getFirestore(app);

    const q = query(collection(db, 'GeoNew'), where('chapter', '==', selectedChapter.value));
    const querySnapshot = await getDocs(q);

    questions.value = querySnapshot.docs.map(doc => {
      const questionData = doc.data();
      questionData.options = Array.isArray(questionData.options) ? questionData.options : [];
      questionData.answer = Array.isArray(questionData.answer) ? questionData.answer : [];
      return questionData;
    });

    
    selectedOptions.value = Array.from({ length: questions.value.length }, () => []);
    answerMessages.value = Array(questions.value.length).fill('');
  } catch (error) {
    console.error('Error getting questions: ', error);
  }
}

function submitAnswers() {
  console.log('user\'s selections：', selectedOptions.value);

  for (let i = 0; i < questions.value.length; i++) {
    const question = questions.value[i];
    const userChoices = selectedOptions.value[i];

    if (question.type === '複選') {
      const correctAnswers = question.answer;

      const isCorrect =
        correctAnswers.length === userChoices.length &&
        correctAnswers.every(answer => userChoices.includes(answer));

      answerMessages.value.splice(i, 1, isCorrect ? `答案正確!!!` : `答案錯誤!!!`);
    }
  }
}
</script>

<template>
  <v-container>
    <v-select
      v-model="selectedChapter"
      :items="['章節一', '章節二']"
      label="請選擇章節"
    ></v-select>

    <div v-for="(question, index) in questions" :key="index">
      <p>{{ question.questionText }}</p>
      <label class="custom-checkbox" v-if="question.type === '複選'" v-for="(option, optionIndex) in question.options" :key="optionIndex">
        <input type="checkbox" :value="option" v-model="selectedOptions[index]">
        {{ option }}
      </label>
      <p>{{ answerMessages[index] }}</p>
    </div>
    <v-btn @click="submitAnswers" color="primary">檢查答案</v-btn>
  </v-container>
</template>

<style scoped>
.custom-checkbox {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
}

.custom-checkbox input {
  margin-right: 8px;
  appearance: none;
  border: 1px solid #000;
  width: 20px;
  height: 20px;
  border-radius: 4px;
  outline: none;
}

.custom-checkbox input:checked {
  background-color: #007BFF;
}
</style>
