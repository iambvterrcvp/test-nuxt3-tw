<template>
  <div
    ref="otp"
    class="mx-auto flex w-full max-w-xs flex-row items-center justify-between"
  >
    <div class="h-14 w-11" v-for="(item, index) in digits">
      <input
        type="text"
        class="flex h-full w-full flex-col items-center justify-center rounded-xl border border-gray-300 bg-white text-center text-lg outline-none ring-pink-600 focus:bg-gray-50 focus:ring-1"
        :key="item + index"
        v-model="digits[index]"
        :autofocus="index === 0"
        maxlength="1"
        pattern="\d*"
        @keydown="(e) => handleKeyDown(e, index)"
      />
    </div>
    <!-- <div class="w-11 h-14">
      <input class="w-full h-full flex flex-col items-center justify-center text-center outline-none rounded-xl border border-gray-300 text-lg bg-white focus:bg-gray-50 focus:ring-1 ring-pink-600" type="number" maxlength="1" pattern="\d*" size="1" autofocus>
    </div>
    <div class="w-11 h-14">
      <input class="w-full h-full flex flex-col items-center justify-center text-center outline-none rounded-xl border border-gray-300 text-lg bg-white focus:bg-gray-50 focus:ring-1 ring-pink-600" type="number" maxlength="1" pattern="\d*" size="1">
    </div>
    <div class="w-11 h-14">
      <input class="w-full h-full flex flex-col items-center justify-center text-center outline-none rounded-xl border border-gray-300 text-lg bg-white focus:bg-gray-50 focus:ring-1 ring-pink-600" type="number" maxlength="1" pattern="\d*" size="1">
    </div>
    <div class="w-11 h-14">
      <input class="w-full h-full flex flex-col items-center justify-center text-center outline-none rounded-xl border border-gray-300 text-lg bg-white focus:bg-gray-50 focus:ring-1 ring-pink-600" type="number" maxlength="1" pattern="\d*" size="1">
    </div>
    <div class="w-11 h-14">
      <input class="w-full h-full flex flex-col items-center justify-center text-center outline-none rounded-xl border border-gray-300 text-lg bg-white focus:bg-gray-50 focus:ring-1 ring-pink-600" type="number" maxlength="1" pattern="\d*" size="1">
    </div>
    <div class="w-11 h-14">
      <input class="w-full h-full flex flex-col items-center justify-center text-center outline-none rounded-xl border border-gray-300 text-lg bg-white focus:bg-gray-50 focus:ring-1 ring-pink-600" type="number" maxlength="1" pattern="\d*" size="1">
    </div> -->
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  count: {
    type: Number,
    default: 6,
  },
  value: {
    type: String,
    default: '',
  },
})

const digits = ref<any[]>([])
const otp = ref<any>(null)

if (props.value && props.value.length === props.count) {
  for (let i = 0; i < props.count; i++) {
    digits.value[i] = props.value.charAt(i)
  }
} else {
  for (let i = 0; i < props.count; i++) {
    digits.value[i] = null
  }
}

function handleKeyDown(event: any, index: number) {
  console.log(event.key, index)
  if (
    event.key !== 'Tab' &&
    event.key !== 'ArrowRight' &&
    event.key !== 'ArrowLeft'
  ) {
    event.preventDefault()
  }

  if (event.key === 'Backspace') {
    console.log(event.key)
    digits.value[index] = null

    if (index != 0) {
      otp.value.children[index - 1].focus()
    }

    return
  }

  if (new RegExp('^([0-9])$').test(event.key)) {
    digits.value[index] = event.key

    if (index != props.count - 1) {
      otp.value.children[index + 1].focus()
    }
  }
}
//https://www.freecodecamp.org/news/create-otp-input-vue-3/
</script>
