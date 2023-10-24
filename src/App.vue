<script setup lang="ts">
import English from "./components/EnglishDB.vue"; 
import Chemistry from "./components/Chemistry.vue";
import ChemistryCheckbox from "./components/ChemistryCheckbox.vue";
import { reactive } from "vue";
let choice = reactive({title:'英文', value:"English"});
let items=[
  {title:'英文', value:"English"},
  {title:'化學', value:"Chemistry"},
  {title:'化學單選', value:"ChemistryCheckbox"}]
</script>

<template>
  <div>
    <v-select label="請選擇" v-model="choice.value" :items="items" item-title="title" item-value="value">
    </v-select>
    <Suspense>
      <English v-if="choice.value === 'English'" />
      <Chemistry v-else-if="choice.value === 'Chemistry'" />
      <ChemistryCheckbox v-else-if="choice.value === 'ChemistryCheckbox'" />
    </Suspense>
  </div>
</template>