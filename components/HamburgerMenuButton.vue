<template>
  <div
    role="button"
    class="relative w-6 h-4 cursor-pointer select-none"
    @click="$emit('toggle', !isOpen)"
  >
    <div
      :class="[
        'absolute w-6 h-0.5 bg-gray-800 right-0 transition-all',
        { 'top-2 rotate-45': isOpen },
        { 'top-0': !isOpen },
      ]"
    />
    <div
      :class="[
        'absolute w-6 h-0.5 bg-gray-800 right-0 transition-all top-2',
        { 'opacity-0': isOpen },
      ]"
    />
    <div
      :class="[
        'absolute w-6 h-0.5 bg-gray-800 right-0 transition-all',
        { 'top-2 -rotate-45': isOpen },
        { 'top-4': !isOpen },
      ]"
    />
  </div>
</template>

<script>
export default {
  name: 'HamburgerMenuButton',
  props: {
    isOpen: {
      type: Boolean,
      default: false,
    },
  },
}
</script>

<style></style>
