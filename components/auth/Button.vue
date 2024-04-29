<template>
  <button
    class="focus:shadow-outline m-auto w-fit rounded-xl bg-pink-600 px-4 py-2 font-bold text-white hover:bg-pink-500 focus:outline-none disabled:bg-pink-300"
    :disabled="disabled"
    type="button"
  >
    {{ label }}
  </button>
</template>

<script setup lang="ts">
defineProps({
  disabled: {
    type: Boolean,
    default: false,
  },
  label: {
    type: String,
    default: '',
  },
})
</script>
