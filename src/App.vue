<script setup>
  import {ref, computed} from 'vue';
  
  const name = "Vue dinamico";

  //counter ahora es una variable reactiva
  const counter = ref(0);
  const arrayFavoritos = ref([]);

  //metodo - methods
  //Aumentar el contador
  const increment = () => {
    counter.value ++;
  }

  //Resetear el contador
  const reset = () => {
    counter.value = 0;
  }

  //Decrementar el contador
  const decrement = () => {
    counter.value --;
  }

  //clase como propiedad computada (recomendada cuando se trabaja con datos reactivos...)
  const classCounter = computed(() => { 
    if (counter.value === 0){
      return 'zero';
    }
    return counter.value > 0 ? 'positive' : 'negative';
  })
  
  //clase como metodo
  const classCounter1 = () => { 
    if (counter.value === 0){
      return 'zero';
    }
    return counter.value > 0 ? 'positive' : 'negative';
  }

  const add = () => { 
    arrayFavoritos.value.push(counter.value);
  }

  const bloquearBtnAdd = computed(() => {
    const numSearch = arrayFavoritos.value.find(num => num === counter.value);
    if(numSearch === 0) return true;
    return numSearch ? true : false;
    //otra forma
    //return numSearch || numSearch === 0
  })
</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter1()">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-secondary">Reset</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
    </div>
    <h2 class="mt-3">Mis Favoritos</h2>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num, index) in arrayFavoritos" :key="index">
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<style>
  h1 {
    color: red;
  }

  .negative {
    color: red;
  }

  .positive {
    color: green;
  }

  .zero {
    color:blueviolet;
  }
</style>