<script setup>
defineProps({
  weatherInfo: Object,
  isDay: Boolean
})
</script>

<template>
  <div class="text-white p-10 rounded-lg shadow-xl gap-6 mb-6 relative bg-blue-400">
    <div class="flex flex-col gap-2">
      <p class="text-2xl font-semibold text-center">
        {{ weatherInfo.location.name }}, {{ weatherInfo.location.country }}
      </p>
      <p class="text-center">{{ weatherInfo.location.localtime }}</p>
    </div>
    <div class="grid place-items-center">
      <img
        :src="weatherInfo.current.condition.icon"
        :alt="weatherInfo.current.condition.text"
        class="object-cover h-28 w-28"
      />
      <p class="text-4xl font-semibold text-center">{{ weatherInfo.current.temp_c }}°C</p>
      <p class="text-center">{{ weatherInfo.current.condition.text }}</p>
    </div>
    <div>
      <p class="text-center">Feels like {{ weatherInfo.current.feelslike_c }}°C</p>
      <p class="text-center">Wind: {{ weatherInfo.current.wind_kph }} km/h</p>
      <p class="text-center">Humidity: {{ weatherInfo.current.humidity }}%</p>
    </div>
    <div>
      <div class="grid grid-cols-3 gap-6 mt-6">
        <div
          v-for="forecast in weatherInfo.forecast.forecastday"
          :key="forecast.date"
          class="border-x-2 border-slate-200 p-2"
        >
          <p class="text-center">{{ new Date(forecast.date).getDate() }}</p>
          <img
            :src="forecast.day.condition.icon"
            :alt="forecast.day.condition.text"
            class="object-cover h-8 w-8 mx-auto"
          />
          <p class="text-center">{{ forecast.day.avgtemp_c }}°C</p>
          <p class="text-center">{{ forecast.day.condition.text }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
