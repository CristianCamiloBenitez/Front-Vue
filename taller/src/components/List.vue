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
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in listaTareas" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.username }}</td>
          </tr>
        </tbody>
    </table>
</template>

<script>
    export default {
        name: 'List',
        data () {
            return {
                listaTareas: []
            }
        },
        methods: {
            async getTareas () {
                const response = await axios.get('https://jsonplaceholder.typicode.com/users')
                //('http://localhost:8080/read/task')
                this.listaTareas = response.data
            }
        },
        created () {
            this.getTareas()
        }
    }

    import axios from 'axios';
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
</style>