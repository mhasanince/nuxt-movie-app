<template>
  <div
    class="relative flex justify-center items-center max-h-[380px] overflow-hidden"
  >
    <div class="container relative mx-auto before-gradient after-gradient">
      <img src="~/assets/img/jumbotron.jpg" alt="Movies" />
    </div>
    <div
      class="absolute w-4/5 -translate-x-1/2 -translate-y-1/2 md:w-1/2 top-1/2 left-1/2"
    >
      <custom-input placeholder="Search for a movie..." @keyup="handleSubmit" />
    </div>
  </div>
</template>

<script>
import CustomInput from '~/components/CustomInput.vue'

export default {
  name: 'JumbotronComponent',
  components: { CustomInput },
  methods: {
    handleSubmit(e) {
      if (e.keyCode === 13) {
        if (e.target.value.length > 0) {
          this.$router.push({
            name: 'movie',
            query: { query: e.target.value },
          })
        } else {
          this.$router.push('/')
        }
        e.target.blur()
      }
    },
  },
}
</script>

<style scoped>
.before-gradient {
  @apply before:absolute before:inset-0 before:bg-gradient-to-r before:from-white -z-10;
}
.after-gradient {
  @apply after:absolute after:inset-0 after:bg-gradient-to-l after:from-white -z-10;
}
</style>
