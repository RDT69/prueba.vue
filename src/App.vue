<template lang="">
  <p>
    Option: 
    <select v-model="options">
      <option value="list">Listado</option>
      <option value="create">Crear tarea</option>
    </select>
  </p>

<div v-if="options=='list'">
<h1>Listado de tareas</h1>
<p>Filtro
  <input type="text" placeholder="Filtro" v-model="wordSerch">
</p>
<p>Nueva tarea: {{newTask}}</p>
<p>Se han encontrado {{tasks.length}} tareas</p>
<p>{{ textoNumeroTareas }}</p>

<!-- Codigo de esta parte en el "ViewTask.vue" -->
<ul>
  <ViewTask
  v-for ="task of filteredTask"
  :key="task.id"
  :task="task"
  @remove-task="removeTask"
  />
</ul>
<!-- Se ayuda de las funciones del script de este codigo. "removeTask" -->

<ul>
  <li v-for="task of tasks" 
    :key="task.id"
    @click="removeTask(task.id)">
    {{task.id}} - {{task.name}}
  </li>
</ul>
</div>

<!-- Codigo de este parte en el "CreateTask.vue" -->
<CreateTask 
v-else 
@insert-Task="insertTask"/> 
<!-- Se ayuda de las funciones del script de este codigo. "insertTask"-->
</template>

<script setup>
import { computed, ref } from 'vue';
import CreateTask from './components/CreateTask.vue';
import ViewTask from './components/ViewTask.vue';

const options = ref('list');
const tasks = ref([
  {
    id: 1,
    name : 'Corregir examenes del lado del servidor.'
  },
  {
    id: 2,
    name : 'Corregir examenes del lado del cliente.'
  },
  {
    id: 3,
    name : 'Corregir examenes de recuperacion.'
  },
  {
    id: 4,
    name : 'Preparar examen de Vue'
  },
]);
const wordSerch = ref('');
const textoNumeroTareas = computed(() => {
if (tasks.value.length==0) return "No hay tareas";
else if (tasks.value.length==1) return "Hay una tarea";
return `Hay ${tasks.value.length} tareas`;
});

const newTask = ref('');

function insertTask(task) {
  console.log('Insertando......');
  console.log(task);
  tasks.value.push({
    id: newId.value,
    name: task
  });
}

const newId = computed(() =>{
const max = Math.max(...tasks.value.map(t => t.id)) + 1;
return max < 0 ? 1: max;
});

function removeTask(id) {
  console.log('Eliminando...' + id);
  tasks.value = tasks.value.filter(t => t.id != id);
}

const v = computed(()=>{
  return tasks.value.filter(t => t.name.toLocaleLowerCase().includes(wordSerch.value.toLocaleLowerCase()));
}); 

</script>
<style lang="">
  
</style>