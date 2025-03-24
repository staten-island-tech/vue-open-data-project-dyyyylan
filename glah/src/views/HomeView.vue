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
  info.value = data;  
  const top10 = data.filter(item => 
  parseInt(item.rnk, 10) <= 10 && item.ethcty === "ASIAN AND PACIFIC ISLANDER"
);

console.log(top10);
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




