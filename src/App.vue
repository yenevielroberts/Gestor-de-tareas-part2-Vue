<script setup>
import {ref} from 'vue'
import TaskList from './components/TaskList.vue';

//Tareas iniciales
const tareas=ref([
  {id:1, nombre:'Aprender Vue', completado:false},
  {id:2, nombre:'Aprender React', completado:true}
])

</script>

<template>
<div id="container">
  <h1>Gestor de tareas</h1>

  <TaskList :tareas="tareas"/>
</div>
</template>

<style scoped>

#container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>











