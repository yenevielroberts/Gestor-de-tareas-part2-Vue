<script setup>
const props=defineProps({
    tarea:{}
})

const emit=defineEmits(['eliminarTarea', 'desmarcarTarea','completarTarea'])

const eliminar=()=>{
    emit('eliminarTarea', props.tarea.id)
}

const completar=()=>{
    emit('completarTarea',props.tarea.id)
}

const descarmarTarea=()=>{
    emit('desmarcarTarea', props.tarea.id)
}
</script>

<template>
    <div class="containerTareas">
        <!--Se aplicara la clase complatada si el valor de completado es true-->
     <p :class="{completada:tarea.completado}">{{ tarea.nombre }}</p>
          <!--Solo se mostrará el boton de completar si el valor de completado es false-->
          <button class="btnsCompletar" v-show="!tarea.completado" @click="completar">Completar</button>
            <!--Solo se mostrará el boton de descarmar si el valor de completado es true-->
           <button v-show="tarea.completado" @click="descarmarTarea"> Desmarcar</button>
          <button class="btnsEliminar" @click="eliminar">Eliminar</button>
        </div>
</template>
<style scoped>

/**Contenedor individual de las tareas */
.containerTareas{

  display: flex;
  flex-direction: row;
  padding: 5px;
  margin: 10px;
  align-items: center;
  border-radius: 10px;
  background-color: #008B8B;
  color:white;
  font-weight: 600;
}

/**Botones */
button{

  margin:5px;
  padding:5px;
  height: fit-content;
  background-color: transparent;
  border: none;
  font-weight: 700;
}

.btnsEliminar:hover{
  font-weight: 700;
  color:red;
}

.btnsCompletar:hover{

  font-weight: 700;
  color:greenyellow;
}


.completada{
  text-decoration-line: line-through;
}
</style>