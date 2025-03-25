<template>
  <form @submit.prevent="Insertar">
    <div v-for="titulo in labels" >
      <label>
        {{ titulo }}
      </label>
      <input type="text" v-model="json[titulo]" />
    </div>
    <button type="submit" >
      Insertar
    </button>
    
    <button type="button" @click="actualizarpersonajes">Actualizar</button>
  </form>
</template>

<script setup>

//import axios from 'axios';

import { defineEmits } from 'vue';

const props = defineProps(['labels','json']);

const emit = defineEmits(['insertar','actualizarpersonajes'])

/*let json = {
  Id: "",
  Nombre: "",
  Rol: "",
  Pelicula: "",
  Descripcion: "",
};*/

const Insertar=() => {

emit('insertar', props.json)

 }

 const actualizarpersonajes = () => {
 emit('actualizarpersonajes', props.json, props.json.Id); 
};
  

</script>
