<script setup>
const props = defineProps({
  error: String,
})
</script>

<template>
  <div class="error" v-if="props.error">{{ props.error }}</div>
</template>

<style scoped>
.error {
  font-size: 18px;
  padding: 15px;
  text-align: center;
  background: var(--bg-card);
  border-radius: 10px;
  margin-top: -49px;
  margin-bottom: 60px;
}
</style>
