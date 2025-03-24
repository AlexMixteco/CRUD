<template>
    <table>
      <thead>
        <tr>
          <th v-for="etiqueta in encabezado" style="border: 1px solid black">
            {{ etiqueta }}
          </th>
        </tr>
        </thead>
      <tbody>
        <tr v-for="inf in info"  style="border: 1px solid black">
          <td v-for="c in claves">{{inf [c]  }}</td>
          <td ><button @click="eliminar(inf.id)">Eliminar</button>
               <button @click="editar(inf)">Editar</button></td>
        </tr>
      </tbody>
    </table>
  </template>
  
  <script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['eliminar','editar'])

 import axios from 'axios';

  const props = defineProps(['encabezado', 'info','claves']);

  const eliminar=(id) => {

  emit('eliminar', id)

   }


  const editar = (inf) => {
  emit('editar', inf); 
  };


  </script>