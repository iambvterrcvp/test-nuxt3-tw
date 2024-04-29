<template>
  <div class="flex flex-col gap-y-6">
    <AuthHeading>
      Confirm Forgot Password
      <template #description>
        <span>This is a sample instruction.</span>
      </template>
    </AuthHeading>
    <AuthOtp @update:otp="(e) => (otp = e)" />
    <div class="flex flex-col gap-y-4">
      <Textfield
        v-model="newPassword"
        label="New Password"
        placeholder="Password"
        :type="ATTR_TYPE_PASSWORD"
      />
      <Textfield
        v-model="confirmNewPassword"
        label="Confirm New Password"
        placeholder="Password"
        :type="ATTR_TYPE_PASSWORD"
      />
    </div>
    <AuthButton
      label="Continue"
      :disabled="!newPassword"
      @click="confirmForgotPassword"
    />
  </div>
</template>

<script setup lang="ts">
import { ATTR_TYPE_PASSWORD } from '~/constants/common'
import { CONFIRM_FORGOT_PASSWORD } from '~/constants/routes'

const otp = ref('')
const newPassword = ref('')
const confirmNewPassword = ref('')

async function confirmForgotPassword() {
  console.log(newPassword.value, otp.value)
  await navigateTo(CONFIRM_FORGOT_PASSWORD)
}

definePageMeta({
  layout: 'auth',
})
</script>
