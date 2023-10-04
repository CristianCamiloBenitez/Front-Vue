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

//
//arrayTareas.value.push()

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
        <div class="row">
          <!-- Primera tabla -->
          <div class="col">
            <table class="table table-bordered">
              <!-- Contenido de la primera tabla aquí -->
            </table>
          </div>
          <!-- Segunda tabla -->
          <div class="col">
            <table class="table table-bordered">
              <!-- Contenido de la segunda tabla aquí -->
            </table>
          </div>
          <!-- Tercera tabla -->
          <div class="col">
            <table class="table table-bordered">
              <!-- Contenido de la tercera tabla aquí -->
            </table>
          </div>
        </div>
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

/* Estilo para las tablas */
table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

table, th, td {
  border: 1px solid #ccc;
}

th, td {
  padding: 8px;
  text-align: left;
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
</style>