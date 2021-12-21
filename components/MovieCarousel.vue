<template>
  <div>
    <h3 class="text-3xl font-bold">{{ title }}</h3>
    <div class="min-h-[340px] lg:px-8">
      <p v-if="$fetchState.pending">Fetching movies...</p>
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
      default: '',
    },
  },
  data() {
    return {
      options: {
        perPageCustom: [
          [0, 1],
          [1024, 2],
          [1420, 3],
        ],
        autoplay: true,
        autoplayTimeout: 5000,
        autoplayHoverPause: true,
        paginationEnabled: false,
        navigationEnabled: true,
        // navigationNextLabel:
        //   '<span class="text-2xl font-black text-orange-500" >></span>',
        // navigationPrevLabel:
        //   '<span class="text-2xl font-black text-orange-500" ><</span>',
        minSwipeDistance: 0,
      },
      movies: [],
    }
  },
  async fetch() {
    this.movies = await fetch(
      `${this.$config.apiURL}/movie${this.fetchUrl}?api_key=${this.$config.apiKey}&language=en-US&page=1`
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

<style>
@media screen and (max-width: 640px) {
  .VueCarousel-navigation > button:first-child {
    left: 16px;
  }
  .VueCarousel-navigation > button:last-child {
    right: 16px;
  }
}
@media screen and (min-width: 640px) {
  .VueCarousel-navigation > button:first-child {
    left: 8px;
  }
  .VueCarousel-navigation > button:last-child {
    right: 8px;
  }
}
</style>
