<template>
  <div
    class="flex flex-col items-center p-5 transition-transform cursor-pointer sm:flex-row hover:scale-105 transform-gpu"
  >
    <img
      :src="image"
      :alt="movie.title"
      class="aspect-[2/3] object-cover rounded-xl h-[300px] drop-shadow-lg bg-white"
    />
    <div
      class="h-[250px] min-h-[150px] w-full sm:w-auto border border-slate-200 rounded-xl p-6 pl-9 -mt-3 sm:mt-0 sm:-ml-3 -z-10 flex-1 shadow-lg shadow-slate-200"
    >
      <ul class="flex flex-col h-full">
        <li class="font-medium line-clamp-3">{{ movie.title }}</li>
        <li class="mt-auto text-sm font-light text-slate-700">
          {{ updatedAt }}
        </li>
        <li class="flex items-center gap-1 -ml-0.5">
          <img src="~/assets/img/star.svg" alt="star" class="w-6 h-6" />
          <p>{{ movie.vote_average }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MovieCardComponent',
  props: {
    movie: {
      type: Object,
      default: () => {},
    },
  },
  computed: {
    image() {
      return this.movie.poster_path
        ? `https://image.tmdb.org/t/p/w300/${this.movie.poster_path}`
        : 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/No-Image-Placeholder.svg/1665px-No-Image-Placeholder.svg.png'
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
