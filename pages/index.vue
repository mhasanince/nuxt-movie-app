<template>
  <div class="flex flex-col gap-6 page-container">
    <movie-carousel
      :title="paths.popular.title"
      :fetch-url="paths.popular.fetchUrl"
    />
    <movie-carousel
      :title="paths.upcoming.title"
      :fetch-url="paths.upcoming.fetchUrl"
    />
  </div>
</template>

<script>
import MovieCarousel from '~/components/MovieCarousel.vue'

export default {
  name: 'IndexPage',
  components: { MovieCarousel },
  data() {
    return {
      paths: {
        popular: {
          title: 'Popular Movies',
          fetchUrl: '/popular',
        },
        upcoming: {
          title: 'Upcoming Movies',
          fetchUrl: '/upcoming',
        },
      },
    }
  },
}
</script>
