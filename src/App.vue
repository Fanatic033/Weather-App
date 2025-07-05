<script setup>
import { onMounted, provide, ref, watch } from 'vue'
import PanelRight from './components/PanelRight.vue'

const API_ENDPOINT = 'https://api.weatherapi.com/v1'

const data = ref()
const error = ref()
const activeIndex = ref(0)
const city = ref('Bishkek')

provide('city', city)

watch(city, () => {
  getCity(city.value)
})

onMounted(() => {
  getCity(city.value)
})

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
</script>

<template>
  <main class="main">
    <div class="left"></div>
    <div class="right">
      <PanelRight
        :data="data"
        :error="error"
        :active-index="activeIndex"
        @select-index="(index) => (activeIndex = index)"
      />
    </div>
  </main>
</template>

<style scoped>
.main {
  display: flex;
  align-items: center;
  justify-content: center;
}
.right {
  background: var(--bg-main);
  padding: 50px 60px;
  border-radius: 25px;
}

.left {
  width: 500px;
  height: 660px;
  border-radius: 30px;
  background: url('/bg.png');
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
