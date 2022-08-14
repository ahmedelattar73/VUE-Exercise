<template>
  <div class="container chart-wrapper">
    <canvas id="myChart" width="400" height="400"></canvas>
  </div>
</template>

<script>
import {Chart, LinearScale, LineController, LineElement, PointElement, Title, CategoryScale} from "chart.js";

export default {
  name: "HistoricalChart",
  props: [
    'historicalData'
  ],
  data(){
    return {
      open: [],
      close: []
    }
  },
  mounted() {
    this.open = this.historicalData.map(item => parseFloat(item.open) )
    this.close = this.historicalData.map(item => parseFloat(item.close))
    const ctx = document.getElementById('myChart').getContext('2d');
    Chart.register(LineController, LineElement, PointElement, LinearScale, Title, CategoryScale);
    new Chart(ctx, {
      type: 'line',
      data: {
        labels: ['open', 'close'],
        datasets: [{
          label: 'open',
          data: this.open,
          backgroundColor: [
            'rgba(255, 99, 132, 0.2)',
            'rgba(54, 162, 235, 0.2)'
          ],
          borderColor: [
            'rgba(255, 99, 132, 1)',
            'rgba(54, 162, 235, 1)'
          ],
          borderWidth: 1
        },
        {
          label: 'closed',
          data: this.close,
          backgroundColor: [
            'rgba(255, 99, 132, 0.2)',
            'rgba(54, 162, 235, 0.2)'
          ],
          borderColor: [
            'rgba(255, 99, 132, 1)',
            'rgba(54, 162, 235, 1)'
          ],
          borderWidth: 1
        }]
      },
      options: {
        scales: {
          y: {
            beginAtZero: true
          }
        }
      }
    });

  }
}
</script>

<style scoped>
  .chart-wrapper {
    height: 300px;
  }
</style>