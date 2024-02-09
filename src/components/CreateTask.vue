<template>
  <p>
    <input type="text" placeholder="Nueva Tarea" @keyup.enter="insertarTask" v-model="newTask">
  </p>
</template>

<script setup>
import {ref} from 'vue';

const newTask = ref('');
const emit = defineEmits(['insertTask']);

function insertarTask(){
  console.log('Insertando...' + newTask.value);
  if (newTask.value.length>2) {
    emit('insertTask', newTask.value);
    newTask.value = '';
  }
}
</script>

<style scoped>
  p {
    background-color: aquamarine;
    padding: 10px;
  }
</style>