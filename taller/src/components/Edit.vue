<template>
    <div>
      <h2>Tareas</h2>
  
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

      <h2>Agregar Comentario y Adjunto</h2>

    <form @submit.prevent="agregarComentarioYAdjunto">
      <label for="comentario">Comentario:</label><br>
      <textarea id="comentario" name="comentario" v-model="comentario"></textarea><br>

      <label for="adjunto">Archivo Adjunto:</label><br>
      <input type="file" id="adjunto" name="adjunto" v-on:change="adjuntoSeleccionado"><br>

      <input type="submit" value="Agregar">
    </form>
  
    </div>
    <div>
      <button @click="goToApp" class="button volver">Volver</button>
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
        comentario: '',
        adjunto: null,
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
        let completed = false; // Por defecto, establece completed como false
        
        if (this.estado === 'Completa') {
          completed = true;
        }

        const datos = {
          id: this.idTarea,
          title: this.nombreTarea,
          description: this.descripcion,
          completed: completed,
        };

        console.log('Datos que se enviarán al servidor:', datos);
        //console.log('ID de la tarea a actualizar:', this.idTarea);

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
      goToApp() {
            // Redirige a la página principal (App.vue)
            window.location.href = '';
      },
      adjuntoSeleccionado(event) {
        this.adjunto = event.target.files[0];
      },
      agregarComentarioYAdjunto() {
        const tareaId = this.idTarea;

        axios.post('http://localhost:8080/write/comments/create',{
          task_id: tareaId,
          comment_text: this.comentario,
        })
        .then((response) => {
          console.log('',response.data);
          this.comentario = '';
        })
        .catch((error) => {
          console.error('Error al crear comentario:', error);
        });

        if (this.adjunto) {
        const formData = new FormData();
        formData.append('task_id', tareaId);
        formData.append('file_name', this.adjunto.name);
        formData.append('file_url', ''); // Debes proporcionar la URL adecuada aquí
        formData.append('file_type', this.adjunto.type);

        // Enviar archivo adjunto al backend
        axios.post('http://localhost:8080/write/attachments/create', formData)
          .then((response) => {
            console.log('Archivo adjunto agregado:', response.data);
            // Limpia el campo de archivo adjunto después de agregarlo
            this.adjunto = null;
          })
          .catch((error) => {
            console.error('Error al agregar archivo adjunto:', error);
          });
        }
      },

    },
    created() {
      this.getTareas();
    },
  };
  </script>
  
  <style>
  @import '../assets/css/bootstrap.css';

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
  