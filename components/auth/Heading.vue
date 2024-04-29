<template>
  <div class="flex flex-col gap-2">
    <div class="text-xl font-semibold text-pink-600">
      <slot />
    </div>
    <div class="text-sm text-gray-600">
      <slot name="description" />
    </div>
  </div>
</template>
