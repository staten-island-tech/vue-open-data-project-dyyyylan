<script>
import { Pie } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement } from 'chart.js'
ChartJS.register(Title, Tooltip, Legend, ArcElement)

export default {
  components: { Pie },
  data() {
    return {
      chartData: {
        labels: ['Red', 'Blue', 'Yellow'],
        datasets: [
          {
            backgroundColor: ['#FF6384', '#36A2EB', '#FFCE56'],
            data: [40, 30, 30]
          }
        ]
      },
      chartOptions: {
        responsive: true,
        plugins: {
          legend: {
            position: 'top'
          }
        }
      }
    }
  }
}
</script>

<template>
  <div>
    <Pie :data="chartData" :options="chartOptions" />
  </div>
</template>