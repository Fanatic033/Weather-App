<script setup>
import { inject, onMounted, ref, watch } from 'vue'
import Button from './Button.vue'
import Input from './Input.vue'

const isEdited = ref(false)

const city = inject('city')
const inputValue = ref(city.value)

function select() {
  isEdited.value = false
  city.value = inputValue.value
}

function edit() {
  isEdited.value = true
}

watch(city, () => {})
</script>

<template>
  <div class="city">
    <div v-if="isEdited" class="city-input">
      <Input placeholder="Введите город" v-model="inputValue" @keyup.enter="select()" v-focus />
      <Button @click="select()">Сохранить</Button>
    </div>
    <Button v-else @click="edit()">
      <img src="/location.svg" alt="Иконка локации" />
      Изменить город
    </Button>
  </div>
</template>

<style scoped>
.city {
  width: 420px;
}
.city-input {
  display: flex;
  gap: 12px;
}
</style>
