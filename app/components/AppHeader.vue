<script setup lang="ts">
const route = useRoute()
const mobileMenuOpen = ref(false)

const items = computed(() => [{
  label: 'Docs',
  to: '/docs',
  active: route.path.startsWith('/docs')
}, {
  label: 'Pricing',
  to: '/pricing'
}, {
  label: 'Blog',
  to: '/blog'
}, {
  label: 'Changelog',
  to: '/changelog'
}])
</script>

<template>
  <header class="border-b border-neutral-200 bg-white">
    <div class="max-w-7xl mx-auto px-6">
      <div class="flex items-center justify-between h-16">
        <!-- Logo -->
        <NuxtLink to="/" class="flex items-center gap-2">
          <AppLogo />
        </NuxtLink>

        <!-- Navigation - Desktop -->
        <nav class="hidden md:flex items-center gap-8">
          <NuxtLink
            v-for="item in items"
            :key="item.to"
            :to="item.to"
            class="text-body-sm font-semibold text-neutral-700 hover:text-blue-50 transition-colors"
            :class="{ 'text-blue-50': item.active }"
          >
            {{ item.label }}
          </NuxtLink>
        </nav>

        <!-- Actions -->
        <div class="flex items-center gap-3">
          <UColorModeButton />

          <NuxtLink
            to="/login"
            class="hidden lg:inline-flex text-body-sm font-semibold text-neutral-700 hover:text-blue-50 transition-colors"
          >
            Sign in
          </NuxtLink>

          <UButton
            label="Sign up"
            to="/signup"
            class="hidden lg:inline-flex bg-blue-50 hover:bg-blue-60 text-white font-semibold"
          />

          <!-- Mobile menu button -->
          <UButton
            icon="i-lucide-menu"
            color="neutral"
            variant="ghost"
            class="lg:hidden"
            @click="mobileMenuOpen = !mobileMenuOpen"
          />
        </div>
      </div>

      <!-- Mobile menu -->
      <nav v-if="mobileMenuOpen" class="md:hidden py-4 border-t border-neutral-200">
        <div class="flex flex-col gap-3">
          <NuxtLink
            v-for="item in items"
            :key="item.to"
            :to="item.to"
            class="text-body-md font-semibold text-neutral-700 hover:text-blue-50 py-2"
            @click="mobileMenuOpen = false"
          >
            {{ item.label }}
          </NuxtLink>
          <USeparator class="my-2" />
          <NuxtLink
            to="/login"
            class="text-body-md font-semibold text-neutral-700 hover:text-blue-50 py-2"
            @click="mobileMenuOpen = false"
          >
            Sign in
          </NuxtLink>
          <UButton
            label="Sign up"
            to="/signup"
            block
            class="bg-blue-50 hover:bg-blue-60 text-white font-semibold"
            @click="mobileMenuOpen = false"
          />
        </div>
      </nav>
    </div>
  </header>
</template>
