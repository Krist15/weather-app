<script setup>
import { reactive, defineEmits } from 'vue'

const state = reactive({
  searchPlace: '',
  data: []
})

const emit = defineEmits(['weatherList'])

const search = async () => {
  const res = await fetch(
    `http://api.weatherapi.com/v1/search.json?key=b2a56c3f83b649dca5434428231306&q=${state.searchPlace}`
  )
  const data = await res.json()
  state.data = data
}

const getPlaceId = async (id) => {
  const res =
    await fetch(`http://api.weatherapi.com/v1/forecast.json?key=b2a56c3f83b649dca5434428231306&q=id:${id}&days=3&aqi=no&alerts=no
`)
  const data = await res.json()
  emit('weatherList', data)
  state.data = []
  state.searchPlace = ''
}
</script>

<template>
  <div class="w-full flex justify-center items-center flex-col">
    <form @submit.prevent="search" class="w-full flex justify-center items-center">
      <div class="w-full flex justify-center items-center">
        <input
          type="text"
          v-model="state.searchPlace"
          class="p-3 w-full md:w-3/5 bg-indigo-100 text-center rounded-lg"
        />
        <button
          type="submit"
          class="p-3 bg-indigo-300 text-white rounded-lg ml-2 hover:bg-indigo-400"
        >
          Search
        </button>
      </div>
    </form>
    <div class="w-full">
      <div
        v-for="item in state.data"
        :key="item.id"
        @click="getPlaceId(item.id)"
        class="rounded-lg w-full h-4 p-5 bg-white text-center flex items-center justify-center my-2 hover:bg-blue-100"
      >
        <button>{{ item.country }}, {{ item.name }}, {{ item.region }}</button>
      </div>
    </div>
  </div>
</template>
