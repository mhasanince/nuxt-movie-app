<template>
  <p v-if="$fetchState.pending">Fetching mountains...</p>
  <p v-else-if="$fetchState.error">An error occurred :(</p>
  <div v-else>
    <h1>{{ movie.title }}</h1>
    <section>similar movies</section>
  </div>
</template>

<script>
export default {
  name: 'MoviePage',
  data() {
    return {
      movie: {},
    }
  },
  async fetch() {
    this.movie = await fetch(
      `https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=cd4eae47349553be3f09c3fe622b8153&language=en-US`
    )
      .then((response) => response.json())
      .catch((error) => console.log(error))
  },
}
</script>

<style></style>
