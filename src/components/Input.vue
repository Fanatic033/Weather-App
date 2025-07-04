<script setup>
const model = defineModel({ type: String })
</script>

<template>
  <input class="input" v-model="model" />
</template>

<style scoped>
.input {
  color: var(--vt-c-white);
  border-radius: 10px;
  border: none;
  width: 260px;
  height: 53px;
  padding: 15px 20px;
  font-size: 18px;
  background: var(--bg-card);
  box-shadow: 1px 2px 4px 0px var(--bg-main);
}
.input::placeholder {
  color: var(--text-placeholder);
}
</style>
