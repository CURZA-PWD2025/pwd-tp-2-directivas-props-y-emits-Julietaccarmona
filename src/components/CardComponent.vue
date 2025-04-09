<template>
  <div>
    <h1>{{ props.pelicula.titulo }}</h1>
    <p>Año: {{ props.pelicula.anio }}</p>
    <p>Género: {{ props.pelicula.genero }}</p>
    <p>Director: {{ props.pelicula.director }}</p>

    <div v-if="props.pelicula.portada">
      <img :src="props.pelicula.portada" alt="Portada de la película" width="200" />
    </div>
    <div v-else>
      <p>Portada no disponible</p>
    </div>

    <p>Likes: {{ props.pelicula.likes }}</p>
    <button @click="toggleLike">
      {{ leDioLike ? 'Quitar like' : 'Dar like' }}
    </button>
  </div>
</template>


<script setup lang="ts">
import { ref } from 'vue';
import Pelicula from '../interfaces/Pelicula';

const props = defineProps<{ pelicula: Pelicula }>();
const emit = defineEmits<{
  (event: 'update_likes', payload: { id: number; likes: number }): void;
}>();

const leDioLike = ref(false);

function toggleLike() {
  leDioLike.value = !leDioLike.value;
  emit('update_likes', {
    id: props.pelicula.id,
    likes: props.pelicula.likes + (leDioLike.value ? 1 : -1),
  });
}
</script>



<style scoped>
img {
  border-radius: 8px;
  box-shadow: 0 0 10px #ccc;
  margin-bottom: 10px;
}
button {
  padding: 5px 10px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>
