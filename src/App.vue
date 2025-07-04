<script setup>
import { computed, ref } from 'vue'
import CitySelect from './components/CitySelect.vue'
import Stat from './components/Stat.vue'
import DayCard from './components/DayCard.vue'
import Error from './components/Error.vue'

const errorMap = new Map([[1006, 'Указаный город не найден']])

const API_ENDPOINT = 'https://api.weatherapi.com/v1'

const data = ref()
const error = ref()
const activeIndex = ref(0)

async function getCity(city) {
  const params = new URLSearchParams({
    q: city,
    lang: 'ru',
    key: 'bfb12779b19e4fff8b485359250307',
    days: 3,
  })
  const response = await fetch(`${API_ENDPOINT}/forecast.json?${params}`)
  const json = await response.json()
  if (response.status !== 200) {
    error.value = json
    data.value = null
  } else {
    data.value = json
    error.value = null
  }
}

const errorDisplay = computed(() => {
  return errorMap.get(error?.value?.error?.code)
})

const dataModified = computed(() => {
  if (!data.value) return []

  return [
    {
      label: 'Влажность',
      stat: data.value.current.humidity + '%',
    },
    {
      label: 'Облачность',
      stat: data.value.current.cloud + '%',
    },
    {
      label: 'Ветер',
      stat: data.value.current.wind_kph + 'км/ч',
    },
  ]
})
</script>

<template>
  <main class="main">
    <Error :error="errorDisplay" />
    <div v-if="data" class="stat-data">
      <div class="stat-list">
        <Stat v-for="item in dataModified" v-bind="item" :key="item.label" />
      </div>
      <div class="day-card-list">
        <DayCard
          v-for="(item, index) in data.forecast.forecastday"
          :key="item.date"
          :weather-code="item.day.condition.code"
          :temp="item.day.avgtemp_c"
          :date="new Date(item.date)"
          :is-active="activeIndex === index"
          @click="() => (activeIndex = index)"
        />
      </div>
    </div>
    <CitySelect @select-city="getCity" />
  </main>
</template>

<style scoped>
.main {
  background: var(--bg-main);
  padding: 50px 60px;
  border-radius: 25px;
}
.day-card-list {
  display: flex;
  gap: 1px;
}

.stat-data {
  display: flex;
  flex-direction: column;
  gap: 80px;
  margin-bottom: 70px;
}

.stat-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
</style>
