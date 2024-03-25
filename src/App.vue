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
  <div class="grid grid-cols-2 gap-5">
    <div v-for="item in weatherPlacesList" :key="item.location.name">
      <Card :item="item" />
    </div>
  </div>
</template>
