<script setup>

import { ref, computed } from 'vue';

import Create from './components/Create.vue'
import List from './components/List.vue';
import Edit from './components/Edit.vue';
import Delete from './components/Delete.vue';
import Search from './components/Search.vue';

const routes = {
  '/list': List,
  '/create': Create,
  '/edit': Edit,
  '/delete': Delete,
  '/search': Search
}
const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() =>{
  return routes[currentPath.value.slice(1) || '/' || ErrorComponent]
})

//metodo
const handleClick = (message) =>{
  console.log(message);
};

//const arrayTareas = ref([])

//arrayTareas.value.push()

/*
metodos
  listarTareas(){

  };

  crearTarea(){

  };
  editarTarea(){

  };
  eliminarTarea(){

  };
  consultar(){

  };*/
</script>

<template>
  <div class="container text-center mt-3">
    <header>
      <h1>Taller CQRS</h1>
    </header>
    <div class="btn-group">
      <a href="#/list" v-on:click="handleClick('Listar Tareas')">Listar</a> |
      <a href="#/create" v-on:click="handleClick('Crear Tarea')">Crear</a> |
      <a href="#/edit" v-on:click="handleClick('Editar Tarea')">Editar</a> |
      <a href="#/delete" v-on:click="handleClick('Eliminar Tarea')">Eliminar</a> |
      <a href="#/search" v-on:click="handleClick('Consultar Tarea')">Consultar</a>
    </div>
    <component :is="currentView"/>
    <main>
      <br/>

      <!---->
      <!--mostrar lista-->
      <!---->

      <!--{{ arrayTareas }}
      <ul class="list-group mt-4">
        <li
        v-for="(tarea, index) in arrayTareas" :key="index">{{ tarea }}</li>
      </ul>
      -->
    </main>
    <footer>
      <p>Copyright 2023</p>
    </footer>
  </div>
  

</template>

<style>

@import './assets/css/bootstrap.css';

body{
  font-family: sans-serif;
}

header{
  background-color:bisque;
  color:black;
  padding: 10px;
}

nav{
  background-color: chartreuse;
  padding: 10px;
}

main{
  padding: 10px;
}

footer{
  background-color: bisque;
  padding: 10px;
}
</style>