<template>
  <div>
    <h1 class="text-3xl font-bold">Search Results</h1>
    <div class="grid grid-cols-1 gap-4 xl:grid-cols-3 lg:grid-cols-2">
      <nuxt-link v-for="(movie, index) in movies" :key="index" :to="to(index)">
        <movie-card :movie="movie" :index="index" />
      </nuxt-link>
    </div>
  </div>
</template>

<script>
import MovieCard from '~/components/MovieCard.vue'
export default {
  name: 'MovieListPage',
  components: { MovieCard },
  data() {
    return {
      movies: [],
    }
  },
  async fetch() {
    this.movies = await fetch(
      `https://api.themoviedb.org/3/search/movie?api_key=cd4eae47349553be3f09c3fe622b8153&language=en-US&page=1&include_adult=false&query=${this.$route.query.query}`
    )
      .then((response) => response.json())
      .then((data) => data.results)
      .catch((error) => console.log(error))
  },
  computed: {
    to() {
      return (index) => `/movie/${this.movies[index].id}`
    },
  },
  watch: {
    $route() {
      this.$fetch()
    },
  },
}
</script>

<style></style>
