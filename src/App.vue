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
  <SearchBar @weather-list="addWeatherPlaceToList" />
  <div class="grid grid-cols-2 gap-6 mt-3">
    <div v-for="weatherInfo in weatherPlacesList" :key="weatherInfo.location.name">
      <Card :weatherInfo="weatherInfo" />
    </div>
  </div>
</template>
