
<script setup lang="ts">
import { ref } from "vue";
import type {Ref} from "vue";


 const name: Ref<string> = ref ('Arturo');
  const age: Ref<number> = ref ('24');
    const erroe: ref ([
      {
        name:"",
      },
    ]);
  const error: Ref<string> = ref ("#d03");

    const validation = () =>{
    if(age.value <18){
      error.value.push({name:'Error', age:''})
    }

    if(name.value.length >18 ){

    }

    }

</script>

<template>
  <main> 
    <div>
      <input @input="validation()" v-model="name"  type="text">
    </div>
    <div> </div>
    <div>
      <input v-model="name"  type="text">
    </div>
    <div>
      <input v-model="age"  type="text">
    </div>

    <h1 :style ="{'color': 'error', 'backgroundColor':'#cd3'}">  {{ name }}</h1>
    <h2 :class="{'error': age > 10}">{{ age }}</h2>
    <h3>Errors</h3>
    <span :v-for="err in errors" :key="index" >
   {{ index }} {{ err }}
    </span>
  </main>
</template>
<style scoped>
.error{
  color: white;
  background-color: red;
  border: 1px solid black;
}

</style>