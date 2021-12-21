<template>
  <p v-if="$fetchState.pending">Fetching movie...</p>
  <p v-else-if="$fetchState.error">An error occurred :(</p>
  <div v-else class="relative">
    <div
      :style="{
        backgroundImage: `url(https://image.tmdb.org/t/p/original${movie.backdrop_path})`,
      }"
      class="backdrop"
    />
    <div class="flex flex-col gap-12 page-container">
      <div
        class="flex flex-col items-center w-full lg:items-start lg:flex-row lg:h-[672px] pt-6"
      >
        <div class="pb-8 lg:pb-0 lg:pr-8">
          <img
            :src="image"
            :alt="imageAlt"
            class="sm:max-w-[400px] rounded-xl drop-shadow-lg shadow-slate-100"
          />
        </div>
        <div class="w-full pt-14 lg:pt-4 lg:pl-4">
          <div class="flex justify-between">
            <h1 class="text-4xl font-bold">{{ movie.title }}</h1>
            <div class="flex flex-col items-end text-orange-500">
              <p class="text-3xl font-bold">{{ movie.vote_average }}/10</p>
              <p>{{ movie.vote_count }}</p>
            </div>
          </div>
          <div
            class="flex flex-col items-center pt-2 m:divide-x-2 sm:pt-0 sm:flex-row"
          >
            <p class="pb-1 font-light sm:pr-2">{{ updatedAt }}</p>
            <div class="flex gap-1 py-1 font-light sm:py-0 sm:px-2">
              <div
                v-for="(genre, index) in movie.genres"
                :key="index"
                class="flex items-center justify-center px-2 py-1 text-xs text-white bg-orange-500 rounded-full cursor-pointer"
              >
                {{ genre.name }}
              </div>
            </div>
            <p class="pt-1 font-medium sm:pt-0 sm:pl-2">{{ movie.runtime }}m</p>
          </div>
          <div class="flex flex-col gap-2 mt-6">
            <blockquote class="p-2 italic border-l-4 border-orange-500">
              {{ movie.tagline }}
            </blockquote>
            <h3 class="text-xl font-semibold">Overview</h3>
            <p>{{ movie.overview }}</p>
          </div>
        </div>
      </div>
      <movie-carousel
        title="Similar Movies"
        :fetch-url="similarMovieFetchUrl"
      />
    </div>
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

<style scoped>
.backdrop {
  @apply absolute top-0 -mt-6 -z-10 before:absolute before:inset-0
  before:bg-orange-500/50 h-[702px] overflow-hidden w-full
  bg-cover bg-center bg-no-repeat opacity-25 hidden sm:block;
}
</style>
