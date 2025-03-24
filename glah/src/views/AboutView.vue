<template>
  <div class="flex flex-col items-center p-6">
    <h2 class="text-2xl font-bold text-gray-800 mb-4">Top 10 Baby Names (Asian & Pacific Islander)</h2>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
      <div v-for="item in top10" :key="item.nm" class="bg-white shadow-md rounded-lg p-4 w-64 text-center">
        <h3 class="text-lg font-semibold text-blue-600">{{ item.gnm }}</h3>
        <p class="text-gray-700"><strong>Rank:</strong> {{ item.rnk }}</p>
        <p class="text-gray-700"><strong>Year:</strong> {{ item.yr }}</p>
        <p class="text-gray-700"><strong>Gender:</strong> {{ item.gndr }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
const top10 = ref([]);
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