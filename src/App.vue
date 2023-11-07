<script setup lang="ts">
//import English from "./components/EnglishDB.vue";
//import Chemistry from "./components/Chemistry.vue";
//import ChemistryRadio from "./components/ChemistryRadio.vue";
//import CitizenTopic from "./components/CitizenTopic.vue";
//import GeographyTopic from "./components/GeographyTopic.vue";
//import { reactive,ref } from "vue";
import { ref } from 'vue'
let drawer = ref(false)
//let choice = reactive({title:'英文', value:"English"});
let items=[
  {title:'英文', to:'/english'},
  {title:'化學', to:'/chemistry'},
  {title:'化學單選', to:'/chemistryRadio'},
  {title:'地理選擇', to:'/geographyTopic'},
  {title:'公民', to:'/citizenTopic'}]
</script>

<template>
  <v-app class="rounded rounded-md">
    <v-app-bar>
      <v-icon icon="plus"></v-icon>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-app-bar-title>Application bar</v-app-bar-title>
    </v-app-bar>
    <v-navigation-drawer floating permanent v-model="drawer">
      <v-list>
        <v-list-item
          v-for="item in items"
          :title="item.title"
          :key="item.title"
          :to="item.to"
        >
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main class="d-flex flex-column align-start justify-start mb-6" style="min-height: 300px">
      <Suspense>
        <RouterView />
      </Suspense>
    </v-main>
  </v-app>
</template>