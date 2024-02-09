<template>
  <li>
    <span>{{ task.id }}:</span> {{ task.name }}
    <button @click="$emit('removeTask', task.id)">Eliminar</button>
    </li>
</template>

<script setup>
defineProps(['task'])
</script>