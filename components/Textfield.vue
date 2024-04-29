<template>
  <div class="w-full">
    <label :for="id" class="mb-2 block text-sm font-medium">{{ label }}</label>
    <div
      class="rounded-lg border border-solid p-4 focus-within:border-gray-500"
    >
      <div
        class="relative grid max-w-full grid-cols-[minmax(0,1fr)_min-content] contain-layout"
      >
        <div class="overflow-hidden break-words">
          <input
            v-model="inputValue"
            class="flex w-full items-center bg-transparent focus:outline-none"
            :id="id"
            :placeholder="placeholder"
            :type="type"
          />
        </div>
        <div v-if="$slots.append" class="flex items-center pl-2">
          <slot name="append" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ATTR_TYPE_TEXT } from '~/constants/common'

const props = defineProps({
  id: {
    type: String,
    default: '',
  },
  label: {
    type: String,
    default: '',
  },
  placeholder: {
    type: String,
    default: '',
  },
  type: {
    type: String,
    default: ATTR_TYPE_TEXT,
  },
  modelValue: {
    type: String,
    default: '',
  },
})

const emits = defineEmits(['update:modelValue'])

const inputValue = computed({
  get() {
    return props.modelValue
  },
  set(newVal) {
    emits('update:modelValue', newVal)
  },
})
</script>
