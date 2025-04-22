<template>
    <div class="mt-6">
      <Line :data="chartData" :options="chartOptions" />
    </div>
  </template>
  
  <script>
  import { Line } from 'vue-chartjs';
  import {
    Chart as ChartJS,
    Title,
    Tooltip,
    Legend,
    LineElement,
    PointElement,
    CategoryScale,
    LinearScale,
  } from 'chart.js';
  
  ChartJS.register(Title, Tooltip, Legend, LineElement, PointElement, CategoryScale, LinearScale);
  
  export default {
    name: 'TemperatureChart',
    components: { Line },
    props: {
      forecast: Array,
    },
    computed: {
      chartData() {
        return {
          labels: this.forecast.map(day => day.datetime),
          datasets: [
            {
              label: 'Temperature (°C)',
              data: this.forecast.map(day => day.temp),
              borderColor: '#1976D2',
              backgroundColor: 'rgba(25, 118, 210, 0.1)',
              fill: true,
              tension: 0.3,
            },
          ],
        };
      },
      chartOptions() {
        return {
          responsive: true,
          plugins: {
            legend: {
              display: true,
            },
          },
          scales: {
            y: {
              title: {
                display: true,
                text: 'Temperature (°C)',
              },
            },
            x: {
              title: {
                display: true,
                text: 'Date',
              },
            },
          },
        };
      },
    },
  };
  </script>
  
  <style scoped>
  canvas {
    max-width: 100%;
  }
  </style>
  