<script setup lang="ts">
import * as z from 'zod'
import type { FormSubmitEvent } from '@nuxt/ui'

definePageMeta({
  layout: 'auth'
})

useSeoMeta({
  title: 'Create account',
  description: 'Create an account to get started'
})

const toast = useToast()

const schema = z.object({
  email: z.email('Enter a valid email address'),
  password: z.string().min(8, 'Must be at least 8 characters'),
  confirm: z.string()
}).refine(data => data.password === data.confirm, {
  message: 'Passwords do not match',
  path: ['confirm']
})

type Schema = z.output<typeof schema>

const state = reactive<Partial<Schema>>({
  email: undefined,
  password: undefined,
  confirm: undefined
})

function onSubmit(event: FormSubmitEvent<Schema>) {
  console.log('Submitted', event.data)
}

function onLoginGov() {
  toast.add({ title: 'Login.gov', description: 'Redirecting to Login.gov...' })
}
</script>

<template>
  <div class="grid grid-cols-1 lg:grid-cols-2 gap-10 lg:gap-16 items-start">
    <!-- Left: Create account form -->
    <div class="max-w-md w-full">
      <h1 class="text-heading-md font-bold text-[#1b1b1b] dark:text-white mb-1">
        Create account
      </h1>
      <p class="text-body-sm text-neutral-600 dark:text-neutral-400 mb-6">
        Create an account or sign up with Login.gov.
      </p>

      <UForm :schema="schema" :state="state" class="space-y-4" @submit="onSubmit">
        <UFormField label="Email address" name="email" required>
          <UInput
            v-model="state.email"
            type="email"
            placeholder="name@example.gov"
            class="w-full"
            size="lg"
          />
        </UFormField>

        <UFormField label="Password" name="password" required>
          <UInput
            v-model="state.password"
            type="password"
            placeholder="At least 8 characters"
            class="w-full"
            size="lg"
          />
        </UFormField>

        <UFormField label="Confirm password" name="confirm" required>
          <UInput
            v-model="state.confirm"
            type="password"
            placeholder="Re-enter your password"
            class="w-full"
            size="lg"
          />
        </UFormField>

        <UButton
          type="submit"
          label="Create account"
          size="lg"
          class="w-full bg-blue-50 hover:bg-blue-60 text-white justify-center font-semibold"
        />
      </UForm>

      <div class="mt-4 flex items-center gap-3">
        <div class="flex-1 h-px bg-neutral-200 dark:bg-neutral-700" />
        <span class="text-xs text-neutral-500">or</span>
        <div class="flex-1 h-px bg-neutral-200 dark:bg-neutral-700" />
      </div>

      <UButton
        label="Sign up with Login.gov"
        size="lg"
        class="w-full mt-4 justify-center bg-blue-10 hover:bg-blue-20 text-blue-70 font-semibold"
        @click="onLoginGov"
      />

      <p class="mt-6 text-body-sm text-neutral-600 dark:text-neutral-400">
        Already have an account?
        <NuxtLink to="/login" class="text-blue-50 hover:underline font-semibold">
          Sign in
        </NuxtLink>
      </p>

      <p class="mt-6 text-body-xs text-neutral-500 dark:text-neutral-400 border-t border-neutral-200 dark:border-neutral-700 pt-4">
        Are you a federal employee?
        <br>
        <NuxtLink to="/" class="text-blue-50 hover:underline">
          Launch enterprise SSO
        </NuxtLink>
      </p>
    </div>

    <!-- Right: Benefits panel -->
    <div class="bg-[#f0f4f9] dark:bg-neutral-800 rounded-lg p-8 lg:p-10">
      <h2 class="text-heading-sm font-bold text-[#1b1b1b] dark:text-white mb-3">
        A tagline that explains the benefit of creating an account.
      </h2>
      <p class="text-body-sm text-neutral-600 dark:text-neutral-400 mb-6">
        Use this space to explain the benefits of your platform through paragraph copy or a bulleted list.
      </p>
      <ul class="space-y-4">
        <li class="flex gap-2 items-start">
          <UIcon name="i-lucide-check" class="text-blue-50 shrink-0 w-5 h-5 self-start translate-y-px" />
          <div>
            <p class="text-body-sm font-semibold text-[#1b1b1b] dark:text-white">Benefit description.</p>
            <p class="text-body-sm text-neutral-500 dark:text-neutral-400">
              Describe how this benefit helps the user accomplish their goals.
            </p>
          </div>
        </li>
        <li class="flex gap-2 items-start">
          <UIcon name="i-lucide-check" class="text-[#005ea2] shrink-0 w-5 h-5 self-start translate-y-px" />
          <div>
            <p class="text-sm font-semibold text-[#1b1b1b] dark:text-white">Benefit description.</p>
            <p class="text-sm text-neutral-500 dark:text-neutral-400">
              Describe how this benefit helps the user accomplish their goals.
            </p>
          </div>
        </li>
        <li class="flex gap-2 items-start">
          <UIcon name="i-lucide-check" class="text-[#005ea2] shrink-0 w-5 h-5 self-start translate-y-px" />
          <div>
            <p class="text-sm font-semibold text-[#1b1b1b] dark:text-white">Benefit description.</p>
            <p class="text-sm text-neutral-500 dark:text-neutral-400">
              Describe how this benefit helps the user accomplish their goals.
            </p>
          </div>
        </li>
      </ul>

      <div class="mt-8 pt-6 border-t border-neutral-200 dark:border-neutral-600">
        <p class="text-body-xs text-neutral-500 dark:text-neutral-400">
          Are you a federal employee?
          <NuxtLink to="/" class="text-blue-50 hover:underline">
            Launch enterprise SSO
          </NuxtLink>
        </p>
      </div>
    </div>
  </div>
</template>
