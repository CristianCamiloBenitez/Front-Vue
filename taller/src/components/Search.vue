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

<script>
import { ref, computed, watch } from 'vue';
import axios from 'axios';

export default {
  name: 'List',
  methods: {
    goToApp() {
            // Redirige a la página principal (App.vue)
            window.location.href = '';
        }
  },
  setup() {
    const listaTareas = ref([]);
    const query = ref(''); // Define 'query' aquí y establece un valor inicial vacío

    const filteredTareas = computed(() => {
      return listaTareas.value.filter(
        (item) =>
          item.title.toLowerCase().includes(query.value.toLowerCase()) || // Buscar por título
          item.id.toString().includes(query.value) || // Buscar por ID
          item.completed.toString().includes(query.value) // Buscar por estado (completada)
      );
    });

    async function getTareas() {
      try {
        const response = await axios.get('http://localhost:8081/read/tasks/get_all');
        listaTareas.value = response.data;
      } catch (error) {
        console.error(error);
      }
    }

    // Llama a la función getTareas al inicio
    getTareas();

    // Watcher para detectar cambios en 'query' y actualizar 'filteredTareas'
    watch(query, () => {
      // No es necesario llamar manualmente a 'getTareas' aquí,
      // ya que el cambio en 'query' activará automáticamente el filtro
    });

    return {
      query,
      filteredTareas,
    };
  },
};
</script>

<template>
  <div>
    <h2>Listar Tareas</h2>
  </div>

  <input v-model="query" placeholder="Buscar tareas" />

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
      <tr v-for="item in filteredTareas" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.title }}</td>
        <td>{{ item.description }}</td>
        <td>{{ item.completed }}</td>
      </tr>
    </tbody>
    <button>Consultar</button>
  </table>

  <h1> Comentarios y Archivos adjuntos</h1>

  <h2>Comentarios</h2>
  <table>
    <thead>
      <tr>
        <th>ID Comentario</th>
        <th>Comentario</th>
      </tr>
    </thead>
    <tbody>
      <!--<tr v-for="item in comentarios" :key="item.id"></tr>-->
      <tr>

      </tr>
    </tbody>
  </table>

  <h2>Archivos Adjuntos</h2>
  <table>
    <thead>
      <tr>
        <th>ID Archivo</th>
        <th>Nombre del Archivo</th>
        <th>Url</th>
        <th>Tipo de Archivo</th>
      </tr>
    </thead>
    <tbody>
      <!--<tr v-for="item in archivos" :key="item.id"></tr>-->
      <tr >

      </tr>
    </tbody>
  </table>
  <div>
    <button @click="goToApp" class="button volver">Volver</button>
  </div>
</template>
