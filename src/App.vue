<script setup>
import { ref, computed } from 'vue';
const name = 'Estoy probando Vue Js por primera vez';
//-----------------------------------
const arrayFrutas = [
    {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",
        stock: 0,
    },
    {
        name: "Pera",
        price: "$2.00",
        description: "Una pera",
        stock: 10,
    },
    {
        name: "Naranja",
        price: "$3.00",
        description: "Una naranja",
        stock: 20,
    },
];
//-----------------------------------
// metodo
const miClick = (message) =>{
  console.log(message)
}
//----------------------------------- VARIABLES REACTIVAS ----------
const contador = ref(0);
const incremento = () =>  contador.value++;
const decremento = () =>  contador.value--;
const reseteo    = () =>  contador.value = 0;
//-----------------------------------COMPUTED----------------------
const classCounter = computed(()=>{
  if(contador.value === 0){
    return 'zero';
  }
  if (contador.value>0) {
    return 'positivo';
  }else{
    return 'negativo';
  }
})
//-----------------------------------TAREA------------------------
const arrayFavoritos = ref([]);
const add = () =>{
  arrayFavoritos.value.push(contador.value); 
}
const bloqueoBtn = computed(()=>{
  const numbusca = arrayFavoritos.value.find((num) =>num === contador.value);
  console.log(numbusca);
  if(numbusca === 0) return true;
  return numbusca ? true : false;
})
</script>

<template>
  <div class="container mt-3">
    <h1>Te saluda Jonathan {{ name }} </h1>
    <ul>
      <template v-for="item in arrayFrutas" 
        :key="item.name">
        <li  v-if="item.stock>0">
          {{ item.name }} {{ item.price }}            
        </li>
      </template>
    </ul>   
    <button v-on:click="miClick('boton 1')" class="btn btn-success">Activame 1</button>
    <button @:click="miClick('boton 2')" class="btn btn-dark">Activame 2</button>

    <h2 :class="classCounter">{{ contador }}</h2> 
    <div class="btn-group">
    <button @click="incremento" class="btn btn-secondary">Incrementar</button>
    <button @click="decremento" class="btn btn-danger">Disminuir</button>
    <button @click="reseteo" class="btn btn-warning">Resetear</button>
    <button @click="add" :disabled="bloqueoBtn" class="btn btn-info">Agregar</button>
    </div>
    
    
    <br>
    {{ arrayFavoritos }}
    <ul class="list-group mt-4">
      <li class="list-group-item"
          v-for="(num ,index) in arrayFavoritos"
        :key="index">
        {{ num }}
      </li>
    </ul>
    
  </div>  
</template>

<style>
  h1{
    color: aqua;
  }
  .positivo{
    color: green;
  }
  .negativo{
    color: red;
  }
  .zero{
    color: blue;
  }
</style>