<template>
  <div>
    <h3 class="text-3xl font-bold">{{ title }}</h3>
    <div class="min-h-[265px] px-8">
      <p v-if="$fetchState.pending">Fetching mountains...</p>
      <p v-else-if="$fetchState.error">An error occurred :(</p>
      <div v-else>
        <client-only>
          <carousel v-bind="options">
            <slide v-for="(movie, index) in movies" :key="index">
              <nuxt-link :to="to(index)">
                <movie-card :movie="movie" :index="index" />
              </nuxt-link>
            </slide>
          </carousel>
        </client-only>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MovieCarouselComponent',
  props: {
    title: {
      type: String,
      default: 'Popular Movies',
    },
    fetchUrl: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      options: {
        perPageCustom: [
          [0, 1],
          [768, 2],
          [1024, 3],
          [1420, 4],
        ],
        autoplay: true,
        autoplayTimeout: 5000,
        autoplayHoverPause: true,
        paginationEnabled: false,
        navigationEnabled: true,
        minSwipeDistance: 0,
      },
      movies: [],
    }
  },
  async fetch() {
    this.movies = await fetch(
      `https://api.themoviedb.org/3/movie/${this.fetchUrl}?api_key=cd4eae47349553be3f09c3fe622b8153&language=en-US&page=1`
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
}
</script>

<style></style>
