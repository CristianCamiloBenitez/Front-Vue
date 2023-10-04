<style>
    @import '../assets/css/bootstrap.css';
</style>


<script>
import { ref, computed } from 'vue';
import { gsap } from 'gsap';

export default {
  setup() {
    const list = [
      { code: '1', name: 'Bruce Lee', description: 'Martial artist' },
      { code: '2', name: 'Jackie Chan', description: 'Actor and martial artist' },
      { code: '3', name: 'Chuck Norris', description: 'Martial artist and actor' },
      { code: '4', name: 'Jet Li', description: 'Martial artist and actor' },
      { code: '5', name: 'Kung Fury', description: 'Action-comedy film character' },
    ];

    const query = ref('');

    const computedList = computed(() => {
      return list.filter(
        (item) =>
          item.name.toLowerCase().includes(query.value) ||
          item.description.toLowerCase().includes(query.value)
      );
    });

    function onBeforeEnter(el) {
      el.style.opacity = 0;
      el.style.height = 0;
    }

    function onEnter(el, done) {
      gsap.to(el, {
        opacity: 1,
        height: '2em',
        delay: el.dataset.index * 0.15,
        onComplete: done,
      });
    }

    function onLeave(el, done) {
      gsap.to(el, {
        opacity: 0,
        height: 0,
        delay: el.dataset.index * 0.15,
        onComplete: done,
      });
    }

    return {
      list,
      query,
      computedList,
      onBeforeEnter,
      onEnter,
      onLeave,
    };
  },
};
</script>



<template>
  <div>
    <h2>Consultar Tareas</h2>
  </div>

  <input v-model="query" />

  <table>
    <thead>
      <tr>
        <th>ID</th>
        <th>Nombre</th>
        <th>Descripción</th>
      </tr>
    </thead>
    <TransitionGroup
      tag="tbody"
      :css="false"
      @before-enter="onBeforeEnter"
      @enter="onEnter"
      @leave="onLeave"
    >
      <tr v-for="(item, index) in computedList" :key="item.code" :data-index="index">
        <td>{{ item.code }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.description }}</td>
      </tr>
    </TransitionGroup>
  </table>
</template>