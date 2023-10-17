<script setup lang="ts">
import Add from "./components/Add.vue";
import Chemistry from "./components/Chemistry.vue";
import ChemistryRadio from "./components/ChemistryRadio.vue";
import Chinese from "./components/Chinese.vue";
import ChemistryCheckbox from "./components/ChemistryCheckbox.vue";
import English from "./components/English.vue";
import { ref } from "vue";
let choice = ref("請選擇");
</script>

<template>
  <div>
    <select v-model="choice">
      <option>請選擇</option>
      <option value="Add">加法</option>
      <option value="Chemistry">化學填空</option>
      <option value="ChemistryRadio">化學單選</option>
      <option value="Chinese">國文單選</option>
      <option value="ChemistryCheckbox">化學複選</option>
      <option value="English">英文複選</option>
    </select>
    <Add v-if="choice === 'Add'" />
    <Chemistry v-else-if="choice === 'Chemistry'" />
    <ChemistryRadio v-else-if="choice ==='ChemistryRadio'"/>
    <ChemistryCheckbox v-else-if="choice ==='ChemistryCheckbox'"/>
    <Chinese v-else-if="choice ==='Chinese'"/>
    <English v-else />
  </div>
</template>