<script setup>

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
      <button @:click="handleClick('Listar Tareas')" class="btn btn-primary">Lista</button>
      <button v-on:click="handleClick('Crear Tareas')">Crear</button>
      <button v-on:click="handleClick('Editar Tareas')">Editar</button>
      <button v-on:click="handleClick('Eliminar Tareas')">Eliminar</button>
      <button v-on:click="handleClick('consultar')">Consultar</button>
    </div>
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