<script setup>
import {ref, reactive} from 'vue'
import TaskList from './components/TaskList.vue';

const checkbox=ref(false);



//Función para marcar las tareas como completadas
const completar=(id)=>{

  const tareaModificar =tareas.value.find(tarea=> tarea.id===id );

  if(tareaModificar){
    tareaModificar.completado=true;
  }

}

//Función para desmarcar las tareas ya completadas
const desmarcar=(id)=>{

  const tareaModificar =tareas.value.find(tarea=> tarea.id===id );

  if(tareaModificar){
    tareaModificar.completado=false;
  }

}

//Función para eliminar las tareas
const eliminar=(id)=>{

  const tareaIndex=tareas.value.findIndex( tarea=>tarea.id===id);

  if(tareaIndex != -1){
    tareas.value.splice(tareaIndex,1);
  }
}


</script>

<template>
<div id="container">
  <h1>Gestor de tareas</h1>

  <TaskList />
</div>
</template>














<style scoped>

#container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

/**Sesion pra agregar tareas */

input[type='text']{

  border-radius: 10px;
  width: 200px;
  height: 20px;
  margin-bottom: 50px;
}

#btnAgregar{
  border-radius: 10px;
  background-color: #228B22;
  padding:5x;
}

#btnAgregar:hover{
  color: white;
}

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


.informe{
  display: flex;
  flex-direction: row;
}

.informe p{
  margin-right: 5px;
  font-weight: bold;
}
</style>
