<script setup>
import { ref } from 'vue'

// Lista inicial de tareas (sin propiedad de completado para esta rama)
const tasks = ref([
  { id: 1, text: 'Aprender conceptos básicos de Git' },
  { id: 2, text: 'Trabajar en la rama feat/nata-tareas' }
])

// Texto para la nueva tarea
const newTaskText = ref('')

// Agregar una nueva tarea a la lista
const addTask = () => {
  const text = newTaskText.value.trim()
  if (!text) return

  tasks.value.push({
    id: Date.now(),
    text: text
  })

  newTaskText.value = ''
}

// Eliminar una tarea por su ID
const removeTask = (id) => {
  tasks.value = tasks.value.filter(task => task.id !== id)
}
</script>

<template>
  <div class="container">
    <header class="header">
      <h1>Sistema de Gestión de Tareas</h1>
    </header>

    <!-- Formulario para agregar tareas -->
    <form @submit.prevent="addTask" class="task-form">
      <input
        v-model="newTaskText"
        type="text"
        placeholder="Escribe una nueva tarea..."
        class="task-input"
      />
      <button type="submit" class="btn btn-add">Agregar</button>
    </form>

    <!-- Mensaje cuando no existen tareas -->
    <div v-if="tasks.length === 0" class="empty-message">
      <p>No hay tareas registradas. ¡Agrega la primera!</p>
    </div>

    <!-- Lista de tareas -->
    <ul v-else class="task-list">
      <li 
        v-for="task in tasks" 
        :key="task.id" 
        class="task-item"
      >
        <span class="task-text">{{ task.text }}</span>
        
        <button 
          @click="removeTask(task.id)" 
          class="btn btn-delete"
          title="Eliminar tarea"
        >
          Eliminar
        </button>
      </li>
    </ul>
  </div>
</template>

