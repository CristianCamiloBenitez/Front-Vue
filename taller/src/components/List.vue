<template>
    <div>
        <h2>Listar Tareas</h2>
    </div>

    <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Nombre Tarea</th>
            <th>Descripción</th>
            <th>Completada</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in listaTareas" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.title }}</td>
            <td>{{ item.description }}</td>
            <td>{{ item.completed }}</td>
          </tr>
        </tbody>
    </table>

    <div>
        <button @click="goToApp" class="button volver">Volver</button>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'List',
    data () {
        return {
            listaTareas: []
        }
    },
    methods: {
        async getTareas () {
            try {
                const response = await axios.get('http://localhost:8081/read/tasks/get_all');
                console.log(response.data);
                this.listaTareas = response.data; // Asume que la respuesta es un array de objetos JSON
            } catch (error) {
                console.error(error);
            }
        },
        goToApp() {
            // Redirige a la página principal (App.vue)
            window.location.href = '';
        }
    },
    created () {
        this.getTareas();
    }
}
</script>

<style>
@import '../assets/css/bootstrap.css';

table {
font-family: arial, sans-serif;
border-collapse: collapse;
width: 100%;
}

td, th {
border: 1px solid #dddddd;
text-align: left;
padding: 8px;
}

tr:nth-child(even) {
background-color: #dddddd;
}

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
