<script setup>
import { onMounted, ref, watch } from 'vue'
import Button from './Button.vue'
import Input from './Input.vue'

const emit = defineEmits(['select-city'])

const city = ref('Bishkek')
const isEdited = ref(false)

onMounted(() => {
  emit('select-city', city.value)
})

function select() {
  isEdited.value = false
  emit('select-city', city.value)
}

function edit() {
  isEdited.value = true
}

watch(city, () => {})
</script>

<template>
  <div class="city">
    <div v-if="isEdited" class="city-input">
      <Input placeholder="Введите город" v-model="city" @keyup.enter="select()" v-focus />
      <Button @click="select()">Сохранить</Button>
    </div>
    <Button v-else @click="edit()">
      <img src="/public/location.svg" alt="Иконка локации" />
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
