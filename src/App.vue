<template>
  <tabla :encabezado='["Id","Nombre","Rol","Pelicula","Descripcion","Botones"]'
  :claves="['id','nombre','rol','pelicula','descripcion']"
  :info="contenidoPersonajes" 
  @eliminar="EliminarPersonajes"
  @editar="mostrarPersonaje"
 />

  <tabla :encabezado='["Id","Nombre","Edad","Nacionalidad","Premios","Botones"]'
  :claves="['id','nombre','edad','nacionalidad','premios']"
  :info="contenidoActores" 
  @eliminar="Eliminaractores"
  @editar="mostrarActor"
 />


  <formulario-personajes
  :labels='["Nombre","Rol","Pelicula","Descripcion"]'
  :json="formPersonajes"
   @insertar="insertarPersonajes"
   @actualizarpersonajes="ActualizarPersonajes"/>

   <formulario-actores
  :labels='["Nombre","Edad","Nacionalidad","Premios"]'
  :json="formActores"
   @insertar="insertarActores"
   @actualizar="ActualizarActores"/>
</template>

<script setup>
import tabla from './components/tabla.vue';
import formularioPersonajes from './components/formularioPersonajes.vue' ;
import formularioActores from './components/formularioActores.vue';
import { ref } from 'vue';
import axios from 'axios';



const formPersonajes = ref({
  Id: '',
  Nombre: '',
  Rol: '',
  Pelicula: '',
  Descripcion: ''
});

const formActores = ref({
  Id: '',
  Nombre: '',
  Edad: '',
  Nacionalidad: '',
  Premios: ''
});

const contenidoPersonajes=ref([]);
const contenidoActores=ref([]);


async function cambiar() {

const options1 = {
    
    method :'GET',
    url: "https://apis-4nl1.onrender.com/api/selectTablas/personajes",
    Headers:{
        'Content-Type':'application/json',
    },
}

const options2 = {
    
    method :'GET',
    url: "https://apis-4nl1.onrender.com/api/selectTablas/actores",
    Headers:{
        'Content-Type':'application/json',
    },
}
try{
    const response = await axios.request(options1)
    const response2 = await axios.request(options2)

    console.log(response.data);
    console.log(response2.data);

    contenidoPersonajes.value=response.data;
    contenidoActores.value=response2.data;
    //return response.data
}
    catch(error){
        console.error("error",error)
        return [{}]
    }
    
}

const Eliminaractores = async (id) => {
   console.log(id);
  const options = {
    method: 'DELETE',
    url: "https://apis-4nl1.onrender.com/api/eliminarActores/"+id,
    headers: {
      'Content-Type': 'application/json',
    },

  }

  try {
    const response = await axios.request(options);

    console.log(response.data);
    cambiar();
       
  } catch (error) {
    console.error("Error", error);
  } 
} 

const EliminarPersonajes = async (id) => {
   console.log(id);
  const options = {
    method: 'DELETE',
    url: "https://apis-4nl1.onrender.com/api/eliminarPersonajes/"+id,
    headers: {
      'Content-Type': 'application/json',
    },

  }

  try {
    const response = await axios.request(options);

    console.log(response.data);
    cambiar();
       
  } catch (error) {
    console.error("Error", error);
  } 
} 

cambiar();


const insertarPersonajes = async (json) => {
console.log(json);
  const options = {
    method: 'POST',
    url: "https://apis-4nl1.onrender.com/api/insertarPersonajes",
    headers: {
      'Content-Type': 'application/json',
    },
    data: json/* {
      id:Id,
      nombre:Nombre,
      rol:Rol,
      pelicula:Pelicula,
      descripcion:Descripcion,
    }, */
  };

  try {
    const response = await axios.request(options);
    console.log(response.data);
    cambiar();
  } catch (error) {
    console.error("Error", error);
  }
};

const insertarActores = async (json) => {
console.log(json);
  const options = {
    method: 'POST',
    url: "https://apis-4nl1.onrender.com/api/insertarActores",
    headers: {
      'Content-Type': 'application/json',
    },
    data: json
  };

  try {
    const response = await axios.request(options);
    console.log(response.data);
    cambiar();
  } catch (error) {
    console.error("Error", error);
  }
};

const mostrarPersonaje = (inf) => {
console.log(inf);
formPersonajes.value.Id = inf.id;
formPersonajes.value.Nombre = inf.nombre;
formPersonajes.value.Rol = inf.rol;
formPersonajes.value.Pelicula = inf.pelicula;
formPersonajes.value.Descripcion = inf.descripcion;


};

const mostrarActor = (inf) => {
console.log(inf);
formActores.value.Id = inf.id;
formActores.value.Nombre = inf.nombre;
formActores.value.Edad = inf.edad;
formActores.value.Nacionalidad = inf.nacionalidad;
formActores.value.Premios = inf.premios;


};

const ActualizarActores = async (json, Id) => {
  console.log("Actualizando actor con ID:", Id); 

  const options = {
    method: 'PUT', 
    url: 'https://apis-4nl1.onrender.com/actualizarActores/' +Id,
    headers: {
      'Content-Type': 'application/json',
    },
    data: json,
  };

  try {
    await axios.request(options);
    cambiar();
  } catch (error) {
    console.error("Error al actualizar:", error);
  }
};

const ActualizarPersonajes = async (json, Id) => {
  console.log("Actualizando personaje con ID:", Id); 

  const options = {
    method: 'PUT', 
    url: 'https://apis-4nl1.onrender.com/api/actualizarPersonajes/' +Id, 
    headers: {
      'Content-Type': 'application/json',
    },
    data: json,
  };

  try {
    await axios.request(options);
    cambiar();
  } catch (error) {
    console.error("Error al actualizar:", error);
  }
};

</script>