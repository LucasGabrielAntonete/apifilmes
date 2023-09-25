<script setup>
import { ref, onMounted } from 'vue'
import api from '@/plugins/axios'


const genres = ref([])

onMounted(async () => {
    try {

        const response = await api.get('genre/tv/list?language=pt-BR')
        genres.value = response.data.genres
    } catch (error) {
        console.log(error)
    }
}) 


</script>

<template>
  <div>
    <h1>Gêneros de programas de TV</h1>
    <ul>
      <li v-for="genre in genres" :key="genre.id">
        {{ genre.name }}
      </li>
    </ul>
  </div>
</template>


<style scoped>
.genre-list {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 2rem;
  list-style: none;
  padding: 0;
}

.genre-item {
  background-color: #5d6424;
  border-radius: 1rem;
  padding: 0.5rem 1rem;
  align-self: center;
  color: #fff;
  display: flex;
  justify-content: center;
}

.genre-item:hover {
  cursor: pointer;
  background-color: #7d8a2e;
  box-shadow: 0 0 0.5rem #5d6424;
}
</style>