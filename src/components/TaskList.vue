<script setup>

import {ref, reactive,computed} from 'vue'
import TaskForm from './TaskForm.vue';

const checkbox=ref(false);

//Tareas iniciales
const tareas=ref([
  {id:1, nombre:'Aprender Vue', completado:false},
  {id:2, nombre:'Aprender React', completado:true}
])


//Función para agregar nuevas tareas
const agregarTarea=(nom)=>{
    console.log(nom)

    //Si la variable nomTarea tiene un valor la agrego la tarea
      const nuevaTarea=reactive({
        id:tareas.value.length+1,
        nombre:nom,
        completado:false
      })

      tareas.value.push(nuevaTarea)
}
</script>

<template>
<div id="container">
    <!--@obtenerTarea es el evento definido en el emit-->
    <TaskForm @obtenerTarea="agregarTarea"/><!--la función agregarTarea le paso como parametro la variable nomTarea que se envia junto con el evento obtenerTarea.-->
 
     <br></br>
    <label for="checkBoxPendiente">Mostras  pendientes</label>
    <input v-model="checkbox" type="checkbox" name="checkBoxPendiente" id="checkBoxPendiente"/>
<!--Pendientes-->
  <section class="listaTareas" v-if="checkbox">
     <div v-for="tarea in tareas" :key="tarea.id">
        <div v-if="!tarea.completado" class="containerTareas">
          <p>{{ tarea.nombre }}</p>
          <!--Solo se mostrará el boton de completar si el valor de completado es false-->
          <button class="btnsCompletar" v-show="!tarea.completado" @click="completar(tarea.id)">Completar</button>
          <button class="btnsEliminar" @click="eliminar(tarea.id)">Eliminar</button>
        </div>
    </div>
  </section>
  <!--Muestra todas las tareas-->
  <section class="listaTareas" v-else>
      <div class="containerTareas" v-for="tarea in tareas" :key="tarea.id" >
        <!--Se aplicara la clase complatada si el valor de completado es true-->
        <p :class="{completada: tarea.completado}">{{ tarea.nombre }}</p>
        <!--Solo se mostrará el boton de descarmar si el valor de completado es true-->
        <button v-show="tarea.completado" @click="desmarcar(tarea.id)"> Desmarcar</button>
         <!--Solo se mostrará el boton de completar si el valor de completado es false-->
        <button class="btnsCompletar" v-show="!tarea.completado" @click="completar(tarea.id)">Completar</button>
        <button class="btnsEliminar" @click="eliminar(tarea.id)" >Eliminar</button>
      </div>
  </section>
</div>
</template>