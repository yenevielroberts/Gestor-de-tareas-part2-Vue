<script setup>
import {ref, computed, reactive} from 'vue'
import TaskList from './components/TaskList.vue';
import TaskForm from './components/TaskForm.vue';

//Tareas iniciales
const tareas=ref([
  {id:1, nombre:'Aprender Vue', completado:false},
  {id:2, nombre:'Aprender React', completado:true}
])

//Función para agregar nuevas tareas
const agregarTarea=(nom)=>{

  //Si la variable nomTarea tiene un valor la agrego la tarea
  if(nom!=null){
    const nuevaTarea=reactive({
      id:tareas.value.length+1,
      nombre:nom,
      completado:false
    })

    tareas.value.push(nuevaTarea)
  }
    
}

const totalTareas=computed(()=> {
  const cantidadTareas=tareas.value.length
  return cantidadTareas

})

const totalPendientes=computed(()=>{

  let tareasPendiente=0

  for(let tarea of tareas.value){

    if(!tarea.completado){
      tareasPendiente++
    }
  }

  return tareasPendiente
})

</script>

<template>
<main id="container">
  <h1>Gestor de tareas</h1>
  <!--@obtenerTarea es el evento definido en el emit-->
  <TaskForm @obtenerTarea="agregarTarea"/><!--la función agregarTarea le paso como parametro la variable nomTarea que se envia junto con el evento obtenerTarea.-->
  <TaskList :tareas="tareas"/>

   <div class="informe">
      <p>Total: {{ totalTareas }} |</p>
      <p>Pendientes {{ totalPendientes }}</p>
  </div>
</main>
</template>

<style scoped>

#container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.informe p{
  margin-right: 5px;
  font-weight: bold;
}
</style>











