<template>
  <div>
    <PieChart/>
  </div>
</template>

<script setup>
import PieChart from '../components/chart.vue'
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




