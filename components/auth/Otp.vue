<template>
  <div
    ref="otp"
    class="mx-auto flex w-full max-w-xs flex-row items-center justify-between"
  >
    <input
      v-for="(item, index) in digits"
      type="text"
      class="flex h-14 w-11 flex-col items-center justify-center rounded-xl border border-gray-300 bg-white text-center text-lg outline-none ring-pink-600 focus:bg-gray-50 focus:ring-1"
      :key="item + index"
      v-model="digits[index]"
      maxlength="1"
      pattern="\d*"
      @keydown="(e) => handleKeyDown(e, index)"
    />
  </div>
</template>

<script setup lang="ts">
const emits = defineEmits(['update:otp'])

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
const otp = ref()

function handleKeyDown(event: any, index: number) {
  if (event.key !== 'Tab') event.preventDefault()

  if (event.key === 'ArrowLeft') {
    otp.value.children[index - 1].focus()
    return
  }

  if (event.key === 'ArrowRight') {
    otp.value.children[index + 1].focus()
    return
  }

  if (event.key === 'Backspace') {
    digits.value[index] = null
    if (index != 0) {
      otp.value.children[index - 1].focus()
      return
    }
  }

  if (new RegExp('^([0-9])$').test(event.key)) {
    digits.value[index] = event.key
    if (index != props.count - 1) {
      otp.value.children[index + 1].focus()
    }
  }

  emits('update:otp', digits.value.join(''))
}

if (props.value && props.value.length === props.count) {
  for (let i = 0; i < props.count; i++) {
    digits.value[i] = props.value.charAt(i)
  }
} else {
  for (let i = 0; i < props.count; i++) {
    digits.value[i] = null
  }
}
</script>
