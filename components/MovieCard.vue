<template>
  <div
    class="flex items-center p-5 transition-transform cursor-pointer hover:scale-105 transform-gpu"
  >
    <img
      :src="image"
      :alt="movie.title"
      class="aspect-[2/3] object-cover rounded-xl h-[225px] drop-shadow-lg bg-white"
    />
    <div
      class="h-[200px] border border-slate-200 rounded-xl p-6 pl-9 -ml-3 -z-10 flex-1 shadow-lg shadow-slate-200"
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
        ? `https://image.tmdb.org/t/p/w200/${this.movie.poster_path}`
        : 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/No-Image-Placeholder.svg/1665px-No-Image-Placeholder.svg.png'
    },
    updatedAt() {
      return this.movie.release_date.replaceAll('-', '/')
    },
  },
}
</script>

<style></style>
