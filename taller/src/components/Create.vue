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

    <div>
      <button @click="goToApp" class="button volver">Volver</button>
    </div>
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
      goToApp() {
            // Redirige a la página principal (App.vue)
            window.location.href = '';
      }
    },
  };
</script>
  
<style>
.button {
  border: none;
  color: white;
  padding: 16px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  transition-duration: 0.4s;
  cursor: pointer;
}

.volver {
  background-color: white; 
  color: black; 
  border: 2px solid #008CBA;
}

.volver:hover {
  background-color: #008CBA;
  color: white;
}
</style>