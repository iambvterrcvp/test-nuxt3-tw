<template>
  <div class="flex flex-col gap-y-6">
    <AuthHeading>
      Forgot Password
      <template #description>
        <span>Please enter your email address to reset your password.</span>
      </template>
    </AuthHeading>
    <Textfield
      v-model="email"
      label="Email Address"
      placeholder="Email Address"
    />
    <AuthButton label="Continue" :disabled="!email" @click="forgotPassword" />
  </div>
</template>

<script setup lang="ts">
import { CONFIRM_FORGOT_PASSWORD } from '~/constants/routes'

const email = ref('')

async function forgotPassword() {
  console.log(email.value)
  await navigateTo(CONFIRM_FORGOT_PASSWORD)
}

definePageMeta({
  layout: 'auth',
})
</script>
