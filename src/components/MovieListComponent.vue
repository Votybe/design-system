<template>
  <div>
    <ul class="container-movies">
      <movie v-for="(movie, index) in movies" :key="index" :movie="movie" class="movie-card"
             @click="goToSingleMovie(movie)"/>
    </ul>
  </div>
</template>

<script lang="ts" setup>
import {defineProps} from "vue";
import Movie from "../components/movie.vue"
import {MovieInterface} from "../interface/Movie";
import {useRoute, useRouter} from 'vue-router'

const router = useRouter()
const route = useRoute()

const props = defineProps({
  movies: Array as () => MovieInterface[]
});

const goToSingleMovie = (movie: MovieInterface) => {
  router.push(`/movie-details/${movie.id}`)
}
</script>

<style lang="scss" scoped>
.container-movies {
  padding: 1rem;
  scroll-behavior: smooth;
  max-height: 90vh;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  overflow-y: auto;

  .movie-card {
    background-color: #333;
    margin: 0.5rem;
    overflow: hidden;
    transition: transform 0.2s ease-in-out;
    width: 195px;

    &:hover {
      scale: 1.02;
      cursor: pointer;
      transition: scale 0.2s ease-in;
    }
  }
}
</style>
