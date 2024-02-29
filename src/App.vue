<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import Honeycomb from './components/Honeycomb.vue';
import { VueSidePanel } from 'vue3-side-panel';
import {ref} from 'vue';

let isOpened = ref(false);
let activeText = ref('');

function showOwner(owner)
{
  console.log(`Clicked a hex owned by ${owner}!`);
  activeText.value = owner;
  isOpened.value = true;
}
</script>

<template>    
<body>
    <div>
      <Honeycomb @hexClick="showOwner"/>
      <VueSidePanel :side="'right'" :rerender="true" width="500px" v-model="isOpened" style="background-color: #ccc">
    <template #default>
      <div style="height: 100%; background-color: #ccc; text-align: center">
        <span style="white-space: pre-wrap; font-size: 24px; background-color: #ccc"> {{ activeText }}</span>
      </div>

    </template>
  </VueSidePanel>
    </div>
</body>
</template>

<style scoped>
body {
  background-image: url("./map.jpg");
  background-repeat: no-repeat;
  background-position: center center;
}
</style>
