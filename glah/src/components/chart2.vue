<script>
import { ref, onMounted } from 'vue';
import { Pie } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement } from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, ArcElement);

export default {
  components: { Pie },
  setup() {
    const chartData = ref({
      labels: [],
      datasets: [
        {
          backgroundColor: ['#FF6384', '#36A2EB', '#FFCE56', '#4BC0C0', '#9966FF'],
          data: []
        }
      ]
    });

    const chartOptions = {
      responsive: true,
      plugins: {
        legend: {
          position: 'top'
        }
      }
    };

    async function fetchChartData() {
      try {
        const response = await fetch('https://data.cityofnewyork.us/resource/25th-nujf.json');
        const data = await response.json();
        const top10 = data
          .filter(item => parseInt(item.rnk, 10) <= 10 && item.ethcty === "ASIAN AND PACIFIC ISLANDER" && item.gndr === "MALE");
        chartData.value.labels = top10.map(item => item.nm);
        chartData.value.datasets[0].data = top10.map(item => parseInt(item.cnt, 10) || 0);
      } catch (error) {
        console.error("Error fetching chart data:", error);
      }
    }

    onMounted(fetchChartData);

    return { chartData, chartOptions };
  }
};
</script>

<template>
  <div class="container">
    <h1>Top 10 Male Asian Baby Names in 2021</h1>
    <Pie v-if="chartData.labels.length" :data="chartData" :options="chartOptions" />
    <p v-else>Loading data...</p>
  </div>
</template>

<style scoped>
.container {
  width: 100vh;
  margin: auto;
  text-align: center;
}
</style>