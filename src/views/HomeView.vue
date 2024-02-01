<script setup lang="ts">
import { ref } from 'vue';
import type { Ref } from 'vue';

const nombre: Ref<string> = ref('');
const apellido: Ref<string> = ref('');
const edad: Ref<number> = ref('');
const genero: Ref<string> = ref('');
  const generonuevo: Ref<string> = ref('');
const errors = ref([]);

const error: Ref<string> = ref('');

const validacion = () => {
  errors.value = [];
  if (nombre.value.length <5) {
    errors.value.push({ nombre: 'Debe de tener mas de 5 menos de 10' });
  }
};

const validacion2 = () => {
  errors.value = [];
    
   if (apellido.value === nombre.value) {
    errors.value.push({ apellido: 'El apellido no puede ser igual al nombre' });
  }
};

const validacion3 = () => {
  errors.value = [];
  if ( edad.value <= 0|| edad.value >=60)   {
    errors.value.push({ edad: 'La edad tiene que ser mayor 0 menor de 60'});
  }
};

const validacion4 = () => {
  errors.value = [];

  if (genero.value === 'otro' && generonuevo.value === '') {
    errors.value.push({ generonuevo: 'Genero nuevo no puede estar vacio' });
  }
};


</script>
<template>
  <main>
    <div>
      <label>Nombre:</label>
      <input @input="validacion()" v-model="nombre" type="text">
    </div>
    <div>
      <label>Apellido:</label>
      <input @input="validacion2()" v-model="apellido" type="text">
    </div>
    <div>
      <label>Edad:</label>
      <input @input="validacion3()" v-model="edad" type="text">
    </div>
    

    <div>
      <label>Genero:</label>
      <select v-model="genero">
        <option value="masculino">Masculino</option>
        <option value="femenino">Femenino</option>
        <option value="otro">Otro</option>
      </select>
    <input v-if="genero === 'otro'" @input="validacion4()" v-model="generonuevo" type="text" placeholder="Ingresa gnero">
    </div>
    <h1 :style="{'color': error }">{{ nombre }}</h1>
    <h2 :class="{'error': apellido === nombre}">{{ apellido }}</h2>
    <h3 :class="{'error': genero === nombre}">{{ genero }}</h3>
    <h4 :class="{'error': edad >10}">{{ edad }}</h4>
    <h5 :class="{'error': genero === 'otro' && errors.some(err => err.generonuevo)}">{{ generonuevo }}</h5>



    <h3>Errors:</h3>
    <span v-for="(err, index) in errors" :key="index">
      {{ err.nombre }} {{ err.apellido }} {{ err.edad }} {{ err.generonuevo }}
    </span>
  </main>
</template>



<style scoped>
  main {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 10px;
    background-color: #0fb9aa;
  }

  div {
    margin-bottom: 15px;
  }

  label {
    display: block;
    font-weight: bold;
    margin-bottom: 5px;
  }

  input,
  select {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  h1, h2, h3, h4 {
    margin-top: 15px;
  }

  h1 {
    font-size: 1.5em;
  }


  h3 {
    margin-top: 15px;
  }

  span {
    display: block;
    color: red;
    margin-top: 5px;
  }


</style>
