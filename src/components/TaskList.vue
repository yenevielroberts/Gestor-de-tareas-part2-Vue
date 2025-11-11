<script setup>

import {ref, reactive,computed} from 'vue'
import TaskForm from './TaskForm.vue';
import TaskItem from './TaskItem.vue';

const props=defineProps({
  tareas:Array
})

const checkbox=ref(false);
//Función para agregar nuevas tareas
const agregarTarea=(nom)=>{

  //Si la variable nomTarea tiene un valor la agrego la tarea
    const nuevaTarea=reactive({
      id:props.tareas.length+1,
      nombre:nom,
      completado:false
    })

    props.tareas.push(nuevaTarea)
}

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

const totalTareas=computed(()=> {
  const cantidadTareas=props.tareas.length
  return cantidadTareas

})

const totalPendientes=computed(()=>{

  let tareasPendiente=0

  for(let tarea of props.tareas){

    if(!tarea.completado){
      tareasPendiente++
    }
  }

  return tareasPendiente
})

</script>

<template>
  <div id="container">
      <!--@obtenerTarea es el evento definido en el emit-->
      <TaskForm @obtenerTarea="agregarTarea"/><!--la función agregarTarea le paso como parametro la variable nomTarea que se envia junto con el evento obtenerTarea.-->
      <br></br>
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

    <div class="informe">
      <p>Total: {{ totalTareas }} |</p>
      <p>Pendientes {{ totalPendientes }}</p>
  </div>
    
  </div>
</template>

<style scoped>
.informe{
  display: flex;
  flex-direction: row;
}

.informe p{
  margin-right: 5px;
  font-weight: bold;
}
</style>