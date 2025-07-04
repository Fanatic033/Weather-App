<script setup>
import { computed } from 'vue'

import IconSun from '@/icons/IconSun.vue'
import IconRain from '@/icons/IconRain.vue'
import IconCloud from '@/icons/IconCloud.vue'

const { weatherCode, temp, date, isActive } = defineProps({
  weatherCode: Number,
  temp: Number,
  date: Date,
  isActive: Boolean,
})

const iconColor = computed(() => {
  return isActive ? 'var(--vt-c-black)' : 'var(--vt-c-white)'
})
</script>

<template>
  <div class="day-card" :class="{ active: isActive }">
    <IconSun v-if="weatherCode <= 1003" :color="iconColor" />
    <IconRain v-if="weatherCode >= 1006 && weatherCode < 1063" :color="iconColor" />
    <IconCloud v-if="weatherCode >= 1063" :color="iconColor" />
    <div class="day-card__day">
      {{ date.toLocaleDateString('ru-Ru', { weekday: 'short' }) }}
    </div>
    <div class="day-card__temp">{{ temp }} ℃</div>
  </div>
</template>

<style scoped>
.day-card {
  width: 100%;
  color: white;
  padding: 20px 24px;
  background: var(--bg-card);
  border-radius: 10px;
  box-shadow: 1px 2px 4px 0 #222831;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 15px;
  font-size: 20px;
  cursor: pointer;
}

.day-card:not(.active):hover {
  background-color: #3a434f;
}

.active {
  background-color: white;
  color: black;
}
.day-card__day {
  font-weight: 400;
}
.day-card__temp {
  font-weight: 700;
}
</style>
