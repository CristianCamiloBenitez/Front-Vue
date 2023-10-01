<template>
    <div>
        <h2>Editar Tareas</h2>
    </div>

    <form action="/action_page.php">
        <label for="fname">First name:</label><br>
        <input type="text" id="fname" name="fname" value="John"><br>
        <label for="lname">Last name:</label><br>
        <input type="text" id="lname" name="lname" value="Doe"><br><br>
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