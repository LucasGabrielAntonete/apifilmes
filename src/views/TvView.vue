<script setup>
import { ref, onMounted } from 'vue'
import api from '@/plugins/axios'


const genres = ref([])
const movies = ref([])

onMounted(async () => {
    try {

        const response = await api.get('genre/tv/list?language=pt-BR')
        genres.value = response.data.genres
    } catch (error) {
        console.log(error)
    }
}) 

const listMovies = async (genreId) => {
    const response = await api.get('discover/tv', {
        params: {
            with_genres: genreId,
            language: 'pt-BR'
        }
    });
    movies.value = response.data.results
};


</script>

<template>
  <div>
    <h1>Gêneros de programas de TV</h1>
    <ul class="genre-list">
      <li class="genre-item" v-for="genre in genres"  @click="listMovies(genre.id)" :key="genre.id">
        {{ genre.name }}
      </li>
    </ul>
  </div>


  <div class="movie-list">
  <div v-for="tv in movies" :key="tv.id" class="movie-card">
    
    <img :src="`https://image.tmdb.org/t/p/w500${tv.poster_path}`" :alt="tv.title" />
    <div class="tv-details">
      <p class="tv-name">{{ tv.name }}</p>
      <p class="tv-release-date">{{ tv.first_air_date }}</p>
      <p class="tv-genres">{{ tv.genre_ids }}</p>
    </div>
    
  </div>
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

.movie-list {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.movie-card {
  width: 15rem;
  height: 30rem;
  border-radius: 0.5rem;
  overflow: hidden;
  box-shadow: 0 0 0.5rem #000;
}

.movie-card img {
  width: 100%;
  height: 20rem;
  border-radius: 0.5rem;
  box-shadow: 0 0 0.5rem #000;
}

.movie-details {
  padding: 0 0.5rem;
}

.movie-title {
  font-size: 1.1rem;
  font-weight: bold;
  line-height: 1.3rem;
  height: 3.2rem;
}

.genre-list {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 2rem;
  list-style: none;
  margin-bottom: 2r
}

</style>