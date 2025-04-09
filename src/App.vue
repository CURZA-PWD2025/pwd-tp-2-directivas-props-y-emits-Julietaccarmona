<script setup lang="ts">
import { ref } from 'vue';
import CardComponent from './components/CardComponent.vue';
import Pelicula from './interfaces/Pelicula';
import moviesData from './movies';

const movies = ref<Pelicula[]>(moviesData);

function updateLikes(payload: { id: number; likes: number }) {
  const peli = movies.value.find(p => p.id === payload.id);
  if (peli) {
    peli.likes = payload.likes;
  }
}
</script>


<template>
  <div class="cards">
    <CardComponent
      v-for="peli in movies"
      :key="peli.id"
      :pelicula="peli"
      @update_likes="updateLikes"
    />
  </div>
</template>


<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
