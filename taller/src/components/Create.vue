<template>
    <div>
        <h2>Crear Tareas</h2>
    </div>
    <form
  class="demo"
  action="/dataCollectionLocation"
  method="post"
  autocomplete="on"
>
    
      <label for="NTask">Nombre Tarea:</label><br>
      <input type="text" id="Ntask" name="NTask" ><br>
      <label for="Description">Descripción:</label><br>
      <input type="text" id="Description" name="Description" ><br><br>
      
      <input type="submit" value="Submit">

</form>

</template>

<script>
    export default {
        name: 'Create',
    }
</script>

<style>
    @import '../assets/css/bootstrap.css';
</style>
