<template>
  <div class="h-dvh w-full">
    <div
      class="absolute bottom-0 left-0 right-0 top-0 m-auto flex w-[600px] flex-col justify-center"
    >
      <div
        class="mb-4 flex flex-col rounded-xl border border-pink-500 bg-white px-8 pb-8 pt-6"
      >
        <slot />
      </div>
    </div>
  </div>
</template>
