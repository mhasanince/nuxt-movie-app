<template>
  <p v-if="$fetchState.pending">Fetching movie...</p>
  <p v-else-if="$fetchState.error">An error occurred :(</p>
  <div v-else class="flex flex-col gap-12">
    <div
      class="flex flex-col items-center w-full divide-y-2 lg:items-start lg:flex-row lg:divide-y-0 lg:divide-x-2 divide-slate-200"
    >
      <div class="pb-8 lg:pr-8">
        <img
          :src="image"
          :alt="imageAlt"
          class="max-w-[400px] rounded-xl drop-shadow-lg shadow-slate-100"
        />
      </div>
      <div class="w-full pt-4 lg:pl-4">
        <div class="flex justify-between">
          <h1 class="text-4xl font-bold">{{ movie.title }}</h1>
          <div class="flex items-center gap-1">
            <img src="~/assets/img/star.svg" alt="star" class="w-12 h-12" />
            <p class="text-xl font-medium">{{ movie.vote_average }}</p>
          </div>
        </div>
        <div class="flex divide-x divide-slate-200">
          <p class="pr-2 font-light text-slate-600">{{ updatedAt }}</p>
          <div class="flex gap-1 px-2 font-light text-slate-600">
            <div
              v-for="(genre, index) in movie.genres"
              :key="index"
              class="px-2 py-1 text-xs text-white bg-orange-500 rounded-full cursor-pointer"
            >
              {{ genre.name }}
            </div>
          </div>
          <p class="pl-2 font-medium text-slate-600">{{ movie.runtime }}m</p>
        </div>
      </div>
    </div>
    <movie-carousel title="Similar Movies" :fetch-url="similarMovieFetchUrl" />
  </div>
</template>

<script>
import MovieCarousel from '~/components/MovieCarousel.vue'
export default {
  name: 'MoviePage',
  components: { MovieCarousel },
  data() {
    return {
      movie: {},
      similarMovies: [],
    }
  },
  async fetch() {
    this.movie = await fetch(
      `${this.$config.apiURL}/movie/${this.$route.params.id}?api_key=${this.$config.apiKey}&language=en-US`
    )
      .then((response) => response.json())
      .catch((error) => console.log(error))
  },
  computed: {
    similarMovieFetchUrl() {
      return `/${this.$route.params.id}/similar`
    },
    image() {
      return this.movie.poster_path
        ? `https://image.tmdb.org/t/p/w400/${this.movie.poster_path}`
        : 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/No-Image-Placeholder.svg/1665px-No-Image-Placeholder.svg.png'
    },
    imageAlt() {
      return this.movie.title
    },
    updatedAt() {
      return this.movie.release_date
        ? this.movie.release_date.replaceAll('-', '/')
        : ''
    },
  },
}
</script>

<style></style>
