<script setup>
defineProps({
  label: String,
  stat: String,
})
</script>

<template>
  <div class="stat">
    <div class="stat-name">{{ label }}</div>
    <div class="stat-value">{{ stat }}</div>
  </div>
</template>

<style scoped>
.stat {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
  font-size: 28px;
}

.stat-name {
  font-weight: 700;
  text-transform: uppercase;
}

.stat-value {
  font-weight: 500;
}
</style>
