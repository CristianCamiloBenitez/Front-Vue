<template>
    <div>
        <h2>Eliminar Tareas</h2>
    </div>

    <select v-model="selected" multiple>
        <option v-for="item in listaTareas" :key="item.id" :value="item.id">{{ item.title }}</option>
    </select>

    <div>Eliminar Tarea de ID: {{ selected }}</div>

    <button @click="eliminarTareas">Eliminar</button>
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
</style>