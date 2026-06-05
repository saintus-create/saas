<script setup lang="ts">
import type { NuxtError } from '#app'

const props = defineProps({
  error: {
    type: Object as PropType<NuxtError>,
    required: true
  }
})

useHead({
  htmlAttrs: { lang: 'en' }
})

useSeoMeta({
  title: 'Page not found',
  description: 'We\'re sorry, the page you are looking for cannot be found.'
})

const { data: navigation } = await useAsyncData('navigation', () => queryCollectionNavigation('docs'), {
  transform: data => data.find(item => item.path === '/docs')?.children || []
})
const { data: files } = useLazyAsyncData('search', () => queryCollectionSearchSections('docs'), {
  server: false
})

const links = [{
  label: 'Docs',
  icon: 'i-lucide-book',
  to: '/docs/getting-started'
}, {
  label: 'Pricing',
  icon: 'i-lucide-credit-card',
  to: '/pricing'
}, {
  label: 'Blog',
  icon: 'i-lucide-pencil',
  to: '/blog'
}]

const is404 = computed(() => props.error?.statusCode === 404)
</script>

<template>
  <div class="min-h-screen flex flex-col bg-white dark:bg-neutral-950">
    <!-- USWDS Official Government Banner -->
    <div class="bg-gray-10 dark:bg-neutral-800 border-b border-neutral-200 dark:border-neutral-700">
      <div class="max-w-7xl mx-auto px-4 py-1 flex items-center gap-2">
        <svg class="w-4 h-4 shrink-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 491.522 491.522">
          <path fill="#BF0A30" d="M0 0h491.522v37.808H0z" />
          <path fill="#FFFFFF" d="M0 37.808h491.522v37.808H0z" />
          <path fill="#002868" d="M0 75.616h245.761v75.616H0z" />
          <path fill="#BF0A30" d="M0 113.425h491.522v37.808H0z" />
          <path fill="#FFFFFF" d="M245.761 75.616h245.761v37.808H245.761z" />
          <path fill="#BF0A30" d="M0 151.233h491.522v37.808H0z" />
          <path fill="#FFFFFF" d="M0 189.041h491.522v37.808H0z" />
        </svg>
        <p class="text-body-xs text-[#1b1b1b] dark:text-neutral-300">
          An official website of the United States government
        </p>
      </div>
    </div>

    <!-- USWDS Site Header -->
    <header class="bg-navy-90 text-white">
      <div class="max-w-7xl mx-auto px-4 py-4 flex items-center justify-between">
        <NuxtLink to="/" class="flex items-center gap-3 hover:opacity-90 transition-opacity">
          <AppLogo class="h-8 w-auto text-white" />
        </NuxtLink>
        <div class="text-right text-body-xs text-blue-20">
          <p class="font-semibold">Agency Contact Center</p>
          <p>(800) 555-0100 • Mon–Fri 8am–6pm ET</p>
        </div>
      </div>
    </header>

    <!-- 404 / Error Content -->
    <main class="flex-1">
      <div class="max-w-3xl mx-auto px-4 py-16">
        <!-- Breadcrumb -->
        <nav class="text-body-xs text-neutral-500 dark:text-neutral-400 mb-8">
          <NuxtLink to="/" class="text-blue-50 hover:underline">Home</NuxtLink>
          <span class="mx-1">/</span>
          <span>Page not found</span>
        </nav>

        <h1 class="text-heading-lg font-bold text-[#1b1b1b] dark:text-white mb-4">
          Page not found
        </h1>

        <p class="text-body-md text-neutral-600 dark:text-neutral-400 mb-2">
          We're sorry, we can't find the page you're looking for. It may have been moved or no longer exists. Try one of the options below.
        </p>

        <p class="text-body-sm text-neutral-500 dark:text-neutral-400 mb-8">
          Error code: {{ error?.statusCode || 404 }}
        </p>

        <div class="flex flex-wrap gap-3 mb-12">
          <UButton
            label="Go back"
            size="lg"
            class="bg-blue-50 hover:bg-blue-60 text-white font-semibold"
            icon="i-lucide-arrow-left"
            @click="() => history.back()"
          />
          <UButton
            label="Continue to homepage"
            size="lg"
            variant="outline"
            class="border-blue-50 text-blue-50 hover:bg-blue-50/5 font-semibold"
            to="/"
          />
        </div>

        <!-- Helpful links -->
        <div class="border-t border-neutral-200 dark:border-neutral-700 pt-8">
          <p class="text-body-sm font-semibold text-[#1b1b1b] dark:text-white mb-4">
            You might be looking for:
          </p>
          <ul class="space-y-2">
            <li v-for="link in links" :key="link.to">
              <NuxtLink
                :to="link.to"
                class="flex items-center gap-2 text-body-sm text-blue-50 hover:underline"
              >
                <UIcon :name="link.icon" class="w-4 h-4" />
                {{ link.label }}
              </NuxtLink>
            </li>
          </ul>
        </div>
      </div>
    </main>

    <!-- USWDS Footer -->
    <footer class="bg-navy-90 text-white">
      <div class="max-w-7xl mx-auto px-4 py-8 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
        <div>
          <AppLogo class="h-6 w-auto text-white mb-2" />
          <p class="text-body-xs text-blue-20">An official website of the U.S. government</p>
        </div>
        <nav class="flex gap-4 text-body-xs text-blue-20 flex-wrap">
          <NuxtLink to="/" class="hover:text-white transition-colors">Contact</NuxtLink>
          <NuxtLink to="/" class="hover:text-white transition-colors">Policies</NuxtLink>
          <NuxtLink to="/" class="hover:text-white transition-colors">Getting started</NuxtLink>
          <NuxtLink to="/" class="hover:text-white transition-colors">About us</NuxtLink>
        </nav>
      </div>
    </footer>

    <ClientOnly>
      <LazyUContentSearch
        :files="files"
        shortcut="meta_k"
        :navigation="navigation"
        :links="links"
        :fuse="{ resultLimit: 42 }"
      />
    </ClientOnly>

    <UToaster />
  </div>
</template>
