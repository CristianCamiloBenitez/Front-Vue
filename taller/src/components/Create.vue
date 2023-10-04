<template>
    <div>
      <h2>Crear Tareas</h2>
    </div>
    <form @submit.prevent="enviarTarea">
      <label for="nombreTarea">Nombre Tarea:</label><br>
      <input type="text" id="nombreTarea" name="nombreTarea" v-model="nombreTarea"><br>
      <label for="descripcion">Descripción:</label><br>
      <input type="text" id="descripcion" name="descripcion" v-model="descripcion"><br><br>
      <input type="submit" value="Submit">
    </form>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'Create',
    data() {
      return {
        nombreTarea: '',
        descripcion: '',
      };
    },
    methods: {
      enviarTarea() {
        const datos = {
          title: this.nombreTarea, // Asegura que coincida con el nombre del atributo esperado en el backend
          description: this.descripcion, // Asegura que coincida con el nombre del atributo esperado en el backend
        };
  
        axios.post('http://localhost:8080/write/tasks/create', datos)
          .then((response) => {
            console.log('Respuesta del servidor:', response.data);
            // Puedes hacer alguna redirección o acción después de enviar con éxito la tarea.
          })
          .catch((error) => {
            console.error('Error al enviar tarea:', error);
          });
      },
    },
  };
  </script>
  
