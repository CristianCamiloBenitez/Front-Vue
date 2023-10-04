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

const showBody = ref(true);

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.hash
})

const currentView = computed(() =>{
  return routes[currentPath.value.slice(1) || '/' || ErrorComponent]
})

const changeComponent = (componentName, message) => {
  console.log(message);
  currentPath.value = `#/${componentName}`;
  showBody.value = false; // Configura showParagraph en false al cambiar de componente
};
</script>

<template>
  <div class="container text-center mt-3">
    <header>
      <h1>Taller CQRS</h1>
    </header>
    <div class="btn-group">
      <!-- Los enlaces para cambiar de componente -->
      <a href="#/list" v-on:click="changeComponent('list', 'Listar Tareas')">Listar</a> 
      <a href="#/create" v-on:click="changeComponent('create', 'Crear Tarea')">Crear</a> 
      <a href="#/edit" v-on:click="changeComponent('edit', 'Editar Tarea')">Editar</a> 
      <a href="#/delete" v-on:click="changeComponent('delete', 'Eliminar Tarea')">Eliminar</a> 
      <a href="#/search" v-on:click="changeComponent('search', 'Consultar Tarea')">Consultar</a>
    </div>
    <component :is="currentView"/>
    
    <div v-if="showBody">
      <h2>Sistema de Gestión de Tareas</h2>
    </div>
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

/* Estilo para la fila de botones */
.btn-group {
  margin-top: 20px;
}

/* Estilo para las columnas que contienen las tablas */
.col {
  margin-bottom: 20px;
}

/* Media query para ajustar el diseño en pantallas más pequeñas */
@media (max-width: 768px) {
  .col {
    width: 100%;
  }
}

a:link, a:visited {
  background-color: #2b90e7;
  color: white;
  padding: 14px 25px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
}

a:hover, a:active {
  background-color: rgb(0, 234, 255);
}

div{
  padding-top: 50px;
  padding-bottom: 50px;
}

h2{
  padding-top: 20px;
  padding-bottom: 50px;
  text-align: center;
  font-size: large;
}
</style>