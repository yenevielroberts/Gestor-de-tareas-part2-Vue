<script setup>
import { computed} from 'vue'
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

  <div class="informe">
    <p>Total: {{ totalTareas }} |</p>
    <p>Pendientes {{ totalPendientes }}</p>
 </div>
</template>