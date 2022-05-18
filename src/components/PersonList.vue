<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';
import { Person } from './Persons.vue'

type Props = {
  persons: Person[]
}

defineProps<Props>()

const emit = defineEmits(['delete'])

const onClickDelete = (id: number) => {
  emit('delete', id)
}
</script>

<template>
  <li v-for="person in persons" :key="person.id" class="person-list">
    <span>{{ person.name }}</span>
    <span>age:{{ person.age }}</span>
    <button @click="onClickDelete(person.id)">
      <span>delete</span>
    </button>
  </li>
</template>

<style scoped>
.person-list {
  list-style-type: none;
  margin-bottom: 12px;
  border-radius: 4px;
  font-size: 20px;
  font-weight: bold;
  display: flex;
  justify-content: space-between ;
  background-color: rgb(251, 231, 255);
  padding: 8px 20px;
  widows: 500px;
}
</style>
