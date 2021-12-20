<template>
  <div class="flex justify-center items-center max-h-[380px] overflow-hidden">
    <div class="container mx-auto relative before-gradient after-gradient">
      <img src="~/assets/img/jumbotron.jpg" alt="Movies" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'JumbotronComponent',
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
