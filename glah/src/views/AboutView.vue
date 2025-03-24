<template>
  <div class="container">
    <h2>Top 10 Female Asian Baby Names in 2021</h2>
    
    <div class="card-list">
      <div v-for="item in top10" :key="item.nm" class="card">
        <h2>{{ item.nm }}</h2>
        <h3>Rank: {{ item.rnk }}</h3>
        <h3>Count: {{ item.cnt }}</h3>
      </div>
    </div>
  </div>
</template>

<script setup>  
import { ref, onMounted } from 'vue';

const info = ref([]);
const top10 = ref([]);

async function getinfo() {
  try {
    let res = await fetch('https://data.cityofnewyork.us/resource/25th-nujf.json');
    let data = await res.json();
    
    info.value = data;
    top10.value = data.filter(item => 
      parseInt(item.rnk, 10) <= 10 && item.ethcty === "ASIAN AND PACIFIC ISLANDER" && item.gndr === "FEMALE"
    );

    console.log("Top 10 Names:", top10.value);
  } catch (error) {
    console.error("There is an error", error);
  }
}

onMounted(() => {
  getinfo();
});
</script>

<style scoped>
.container {
  text-align: center;
  margin: 20px;
}

.card-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 15px;
}

.card {
  background: #f9f9f9;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  width: 200px;
}
</style>