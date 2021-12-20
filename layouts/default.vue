<template>
  <div class="flex flex-col min-h-screen antialiased">
    <header class="shadow-lg shadow-slate-100">
      <div
        class="container flex items-center justify-between py-4 mx-auto padding-x"
      >
        <img src="~/assets/img/appcent-logo.svg" alt="Appcent" />
        <nav class="hidden sm:block">
          <ul class="flex gap-4 text-xl font-bold">
            <li
              v-for="(item, index) in menuItems"
              :key="index"
              :class="[
                { 'underline text-orange-500': $route.path === item.to },
                'hover:text-orange-500',
              ]"
            >
              <router-link :to="item.to">{{ item.text }}</router-link>
            </li>
          </ul>
        </nav>
      </div>
    </header>
    <main>
      <jumbotron v-if="showJumbotron" />
      <div class="container mx-auto my-6 padding-x">
        <Nuxt />
      </div>
    </main>
    <custom-footer />
  </div>
</template>

<script>
import Jumbotron from '~/components/Jumbotron.vue'
import CustomFooter from '~/components/CustomFooter.vue'

export default {
  name: 'DefaultLayout',
  components: { Jumbotron, CustomFooter },
  data() {
    return {
      menuItems: [
        { text: 'Homepage', to: '/' },
        { text: 'About', to: '/about' },
      ],
    }
  },
  computed: {
    showJumbotron() {
      return this.$route.path === '/' || this.$route.path === '/movie'
    },
  },
}
</script>

<style scoped>
.padding-x {
  @apply px-2 md:px-4;
}
</style>
