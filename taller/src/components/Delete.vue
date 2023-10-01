<template>
    <div>
        <h2>Eliminar Tareas</h2>
    </div>

    <div>Eliminar: {{ selected }}</div>

  <select v-model="selected" multiple>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
</template>

<script>
    export default {
        name: 'Delete',
    }
</script>

<script setup>
    import { ref } from 'vue';

    const selected = ref([])
</script>

<style>
    @import '../assets/css/bootstrap.css';

    select[multiple] {
        width: 100px;
    }
</style>