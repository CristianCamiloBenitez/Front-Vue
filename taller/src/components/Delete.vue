<template>
    <div>
        <h2>Eliminar Tareas</h2>
    </div>

    <select v-model="selected" multiple>
        <option v-for="item in listaTareas" :key="item.id" :value="item.id">{{ item.title }}</option>
    </select>

    <div>Eliminar Tarea de ID: {{ selected }}</div>

    <button @click="eliminarTareas">Eliminar</button>

    <div>
        <button @click="goToApp" class="button volver">Volver</button>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'Delete',
    data () {
        return {
            listaTareas: [],
            selected: [] // Array para almacenar las tareas seleccionadas
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
        async eliminarTareas() {
            try {
                for (const taskId of this.selected) {
                    await axios.delete(`http://localhost:8080/write/tasks/delete/${taskId}`);
                }
                // Después de eliminar, actualiza la lista de tareas
                await this.getTareas();
                // Limpia la selección
                this.selected = [];
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

    select[multiple] {
        width: 100px;
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