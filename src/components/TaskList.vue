<script setup>

import {ref} from 'vue'

import TaskItem from './TaskItem.vue';

const props=defineProps({
  tareas:Array
})

const checkbox=ref(false);


//Función para eliminar las tareas
const eliminar=(id)=>{

  let confirmar=confirm('¿Seguro que quieres eliminar está tarea?')

  if(confirmar){
     const tareaIndex=props.tareas.findIndex( tarea=>tarea.id===id);

    if(tareaIndex != -1){
      props.tareas.splice(tareaIndex,1);
    }
  }
 
}

//Función para desmarcar las tareas ya completadas
const desmarcar=(id)=>{

  const tareaModificar =props.tareas.find(tarea=> tarea.id===id );

  if(tareaModificar){
    tareaModificar.completado=false;
  }
}

//Función para marcar las tareas como completadas
const completar=(id)=>{

  const tareaModificar =props.tareas.find(tarea=> tarea.id===id );

  if(tareaModificar){
    tareaModificar.completado=true;
  }

}

</script>

<template>
  <div id="container">
      <label for="checkBoxPendiente">Mostras  pendientes</label>
      <input v-model="checkbox" type="checkbox" name="checkBoxPendiente" id="checkBoxPendiente"/>

      <!--Lista de tareas-->
      <section v-for="tarea in tareas" :key="tarea.id">

        <!--Pendientes-->
        <section v-if="checkbox" class="listaTareas">
          <div v-show="!tarea.completado">
            <TaskItem :tarea="tarea" @eliminarTarea="eliminar" @desmarcarTarea="desmarcar" @completarTarea="completar"/>
          </div>
        </section>
        
        <!--Todas las tareas-->
        <section v-else class="listaTareas">
          <TaskItem :tarea="tarea" @eliminarTarea="eliminar" @desmarcarTarea="desmarcar" @completarTarea="completar"/>
        </section>
      </section>
  </div>
</template>

<style scoped>
.informe{
  display: flex;
  flex-direction: row;
}
</style>