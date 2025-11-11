<script setup>
import { computed} from 'vue'

const props=defineProps({
  tareas:Array
})
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

  <div class="informe">
    <p>Total: {{ totalTareas }} |</p>
    <p>Pendientes {{ totalPendientes }}</p>
 </div>
</template>