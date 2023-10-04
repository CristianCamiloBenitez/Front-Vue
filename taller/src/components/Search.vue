<style>
    @import '../assets/css/bootstrap.css';
</style>

<script>
import { ref, computed } from 'vue';
import axios from 'axios';

export default {
  name: 'List',
  data() {
    return {
      listaTareas: [],
      query: '',
      filteredTareas: [],
    };
  },
  setup() {
    const listaTareas = ref([]);
    const query = ref('');

    const filteredTareas = computed(() => {
      return listaTareas.value.filter(
        (item) =>
          item.title.toLowerCase().includes(query.value) ||
          item.description.toLowerCase().includes(query.value)
      );
    });

    async function getTareas() {
      try {
        const response = await axios.get('http://localhost:8081/read/tasks/get_all');
        console.log(response.data);
        listaTareas.value = response.data;
      } catch (error) {
        console.error(error);
      }
    }

    // Llama a la función getTareas en el setup
    getTareas();

    return {
      listaTareas,
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
  </table>
</template>
