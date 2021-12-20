<template>
  <input
    class="w-full px-4 py-2 text-xl bg-white border rounded shadow-lg shadow-slate-100 outline-orange-400"
    @keyup="$emit('keyup', $event)"
  />
</template>

<script>
export default {
  name: 'CustomInputComponent',
}
</script>

<style></style>
