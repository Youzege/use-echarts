<template>
  <div class="wrapper">
    <BarChart :boxOfficeData="boxOfficeData" class="chart" />
    <DoughnutChart :boxOfficeData="boxOfficeData" class="chart" />
  </div>
</template>

<script setup>
import BarChart from './components/BarChart.vue'
import DoughnutChart from "./components/DoughnutChart.vue"

import { onMounted, ref, watchEffect } from 'vue'

const boxOfficeData = ref([])

const fetchData = async () => {
  const res = await fetch('http://127.0.0.1:4523/mock/695807/charts')
  const data = await res.json()
  boxOfficeData.value = data.sort((a, b) => b.boxOffice - a.boxOffice)
}

onMounted(() => {
  fetchData()
})
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background: hsl(210deg, 20%, 10%);
}

.wrapper {
  width: 100vw;
  height: 100vh;
  display: grid;
  place-items: center;
  .chart {
    width: 50%;
    height: 70%;
  }
}
</style>
