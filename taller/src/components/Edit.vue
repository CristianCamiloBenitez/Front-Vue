<template>
    <div>
        <h2>Editar Tareas</h2>
    </div>

    <form action="/action_page.php">
        <label for="NTask">Nombre Tarea:</label><br>
        <input type="text" id="Ntask" name="NTask" ><br>
        <label for="Description">Descripción:</label><br>
        <input type="text" id="Description" name="Description" ><br><br>
        <select id="estado" name="estado">
        <option value="Completa">Completa</option>
        <option value="En Progreso">En Progreso</option>
        </select>
        <input type="submit" value="Submit">
    </form> 
</template>

<script>
    export default {
        name: 'Edit',
    }
</script>

<style>
    @import '../assets/css/bootstrap.css';
</style>