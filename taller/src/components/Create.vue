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
    <div class="form-item">
    <label for="name">Full Name:</label>
    <input
      type="text"
      name="name"
      id="name"
      v-model="name"
      aria-labelledby="billing name"
      aria-describedby="nameDescription"
    />
    <p id="nameDescription">Please provide first and last name.</p>
  </div>
  <button type="submit">Submit</button>
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