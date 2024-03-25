<script setup>
import { reactive } from 'vue'
import ListComponent from './ListComponent.vue'

const state = reactive({
  searchPlace: '',
  data: []
})

const search = async () => {
  const res = await fetch(
    `http://api.weatherapi.com/v1/search.json?key=b2a56c3f83b649dca5434428231306&q=${state.searchPlace}`
  )
  const data = await res.json()
  console.log(data)

  state.data = data
}

const getPlaceId = (id) => {
  console.log(id)
}
</script>

<template>
  <div class="w-full flex justify-center items-center flex-col">
    <form @submit.prevent="search" class="w-full flex justify-center items-center">
      <input
        type="text"
        v-model="state.searchPlace"
        class="p-3 w-3/4 bg-gray-200 text-center rounded-lg"
      />
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
