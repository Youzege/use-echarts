<template>
  <Chart :options="options" />
</template>

<script setup>
import Chart from './Chart.vue'
import barChartOptionCreator from '../charts/barChart.js'
import { computed, toRefs } from 'vue'

const props = defineProps({
  boxOfficeData: Array
})

const { boxOfficeData } = toRefs(props)

const options = computed(() => {
  const { names, boxOffices } = populateMovieData(boxOfficeData.value)
  return barChartOptionCreator(names, boxOffices)
})

function populateMovieData (rawData) {
  let names = []
  let boxOffices = []
  rawData.forEach(movie => {
    names.push(movie?.name)
    boxOffices.push(movie?.boxOffice)
  })

  return { names, boxOffices }
}
</script>

<style lang="scss" scoped></style>
