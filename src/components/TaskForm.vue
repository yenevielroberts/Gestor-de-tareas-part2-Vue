<script setup>
import {ref} from 'vue'

const nomTarea=ref('');

const emit=defineEmits(['obtenerTarea'])//defino mi evento

const obtenerTarea=()=>{
    emit ('obtenerTarea',nomTarea.value)
}
</script>

<template>
 <section class="sectionAgregarTarea">
    <input v-model="nomTarea" type="text" id="nomTarea" name="nomTarea" placeholder="Escribe una nueva tarea"/>
    <button id="btnAgregar" @click="obtenerTarea">Agregar</button>
 </section>
</template>