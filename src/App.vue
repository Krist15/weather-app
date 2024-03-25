<script setup>
import { ref } from 'vue'
import SearchBar from './components/SearchBar.vue'
import Card from './components/Card.vue'

const weatherPlacesList = ref([])

const addWeatherPlaceToList = (data) => {
  weatherPlacesList.value.push(data)
}
</script>

<template>
  <div class="grid place-content-center">
    <h1
      class="text-4xl font-semibold text-center text-white bg-indigo-300 shadow-xl rounded-lg p-2 mb-3"
    >
      Weather App 🌦️
    </h1>
  </div>
  <SearchBar @weather-list="addWeatherPlaceToList" />
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mt-3">
    <div v-for="weatherInfo in weatherPlacesList" :key="weatherInfo.location.name">
      <Card :weatherInfo="weatherInfo" />
    </div>
  </div>
</template>
