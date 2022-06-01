<script setup lang="ts">
import { ref, defineEmits, computed } from 'vue'

//
// Variables
//
const inputtingName = ref<string>('')
const inputtingAge = ref<number>(0)

//
// Functions
//
const emit = defineEmits (['register'])

const register = () => {
  const person = { id: Math.random(), name: inputtingName.value, age: inputtingAge }
  emit('register', person)
}

const isValidName = computed(() => {
  if (inputtingName.value.length >= nameLengthLimit) {
    return false
  } else {
    return true
  }
})

const nameLengthLimit = 15
const color = computed(() => {
  return isValidName.value ? 'white' : 'rgb(244,194,190)'
})

</script>

<template>
  <div class="form-container">
    <div class="input-container">
      <div class="input-column">
        <span>name:</span>
        <input class="input-name" v-model="inputtingName"/>
      </div>
      <span class="error-message" v-if="!isValidName">{{ nameLengthLimit }} character or less, please</span>
      <div class="input-column">
        <span>age:</span>
        <input class="input" v-model="inputtingAge" type="number"/>
      </div>
    </div>
    <button @click="register" class="register-button" :disabled="!isValidName">register</button>
  </div>
</template>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgb(235, 255, 231);
  padding: 24px 0;
  width: 50%;
  margin-bottom: 12px;
  border-radius: 4px;
}

.input-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 50px;
  margin-bottom: 20px;
}

.input-column {
  width: 200px;
  display: flex;
  justify-content: space-between;
}

input {
  width: 120px;
  margin-bottom: 12px;
}

.input-name {
  background-color: v-bind(color);
  width: 120px;
  margin-bottom: 12px;
}

.error-message {
  font-size: 12px;
  color: rgb(244,194,190)
}

span {
  font-size: 20px;
  font-weight: bold;
}
</style>
