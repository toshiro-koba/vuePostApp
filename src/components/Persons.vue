<script setup lang="ts">
import { ref, Ref } from 'vue';
import PersonPostForm from './PersonPostForm.vue';
import PersonList from './PersonList.vue';

//
// Types
//
export type Person = {
  id:   number,
  name: string,
  age:  number
}

//
// Variables
//
const persons: Ref<Person[]> = ref([{ id: 0, name: 'John', age: 24 }, { id: 1, name: 'Saki', age: 25 }])

//
// Functions
//
const registerPerson = (person: Person) => {
  persons.value.push(person)
}

const deletePerson = (id: number) => {
  persons.value = persons.value.filter(p => p.id !== id)
}
</script>

<template>
  <h1>Persons</h1>
  <div class="container">
    <PersonPostForm @register="registerPerson"/>
    <div class="list-container">
      <ul>
        <PersonList :persons="persons" @delete="deletePerson" />
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
