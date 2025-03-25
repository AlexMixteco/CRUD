<template>
    <form @submit.prevent="Insertar">
      <div v-for="titulo in labels" >
        <label>
          {{ titulo }}
        </label>
        <input type="text" v-model="json[titulo]" />
      </div>
      <button type="submit">
        Insertar
      </button>
      <button type="button" @click="actualizar">Actualizar</button>
    </form>
  </template>
  
  <script setup>
  
 //import axios from 'axios';
  
  import { defineEmits } from 'vue';
  
  const props = defineProps(['labels','json']);
  
  const emit = defineEmits(['insertar','actualizar'])
  
  /*let json = {
    Nombre: "",
    Edad: "",
    Nacionalidad: "",
    Premios: "",
    
  };*/
  
  const Insertar=() => {
  
  emit('insertar', props.json)
  
   }


  const actualizar = () => {
  emit('actualizar', props.json, props.json.Id); 
};
  
  </script>