<template>
  <div>
<h1 v-for="(item, index) in info" :key="index">
  {{ item.nm }}
</h1>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
const info = ref([])
async function getinfo() {
  try {
      let res = await fetch('https://data.cityofnewyork.us/resource/25th-nujf.json')
  let data = await res.json();
  console.log(data);
  info.value = data;
  }
  catch(error) {
    console.error("there is an error", error); 
  }
}
onMounted(()=> {
  getinfo();
})
</script>

<style scoped>

</style>