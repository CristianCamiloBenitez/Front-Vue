<template>
    <div>
      <h2>Lista de Tareas</h2>
  
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Nombre Tarea</th>
            <th>Descripción</th>
            <th>Completada</th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in listaTareas" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.title }}</td>
            <td>{{ item.description }}</td>
            <td>{{ item.completed }}</td>
            <td>
              <button @click="editarTarea(item)">Editar</button>
            </td>
          </tr>
        </tbody>
      </table>
  
      <h2>Editar Tarea</h2>
  
      <form @submit.prevent="actualizarTarea">
        <input type="hidden" v-model="idTarea">
        
        <label for="nombreTarea">Nombre Tarea:</label><br>
        <input type="text" id="nombreTarea" name="nombreTarea" v-model="nombreTarea"><br>
        
        <label for="descripcion">Descripción:</label><br>
        <input type="text" id="descripcion" name="descripcion" v-model="descripcion"><br><br>
    
        <label for="estado">Estado:</label><br>
        <select id="estado" name="estado" v-model="estado">
          <option value="Completa">Completa</option>
          <option value="En Progreso">En Progreso</option>
        </select>
    
        <input type="submit" value="Actualizar">
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'Tareas',
    data() {
      return {
        listaTareas: [],
        idTarea: '',
        nombreTarea: '',
        descripcion: '',
        estado: true, // Cambiado a un valor booleano
      };
    },
    methods: {
      async getTareas() {
        try {
          const response = await axios.get('http://localhost:8081/read/tasks/get_all');
          console.log(response.data);
          this.listaTareas = response.data;
        } catch (error) {
          console.error(error);
        }
      },
      editarTarea(item) {
        this.idTarea = item.id;
        this.nombreTarea = item.title;
        this.descripcion = item.description;
        this.estado = item.completed; // Asignar directamente el valor booleano
      },
      actualizarTarea() {
        const datos = {
          title: this.nombreTarea,
          description: this.descripcion,
          completed: this.estado, // Asignar directamente el valor booleano
        };
  
        axios.put(`http://localhost:8080/write/tasks/update/${this.idTarea}`, datos)
          .then((response) => {
            console.log('Tarea actualizada:', response.data);
            // Actualizar la lista de tareas después de la edición
            this.getTareas();
          })
          .catch((error) => {
            console.error('Error al actualizar tarea:', error);
          });
      },
    },
    created() {
      this.getTareas();
    },
  };
  </script>
  
  
  
  <style>
  @import '../assets/css/bootstrap.css';
  </style>
  