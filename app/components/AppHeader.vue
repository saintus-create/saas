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
  <header class="fixed top-0 left-0 right-0 z-50 bg-[#0b0d11]/80 backdrop-blur-md border-b border-white/[0.04]">
    <div class="max-w-5xl mx-auto px-6">
      <div class="flex items-center justify-between h-14">
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
            class="text-body-sm text-white/35 hover:text-white/70 transition-colors"
            :class="{ 'text-white/70': item.active }"
          >
            {{ item.label }}
          </NuxtLink>
        </nav>

        <!-- Actions -->
        <div class="flex items-center gap-4">
          <NuxtLink
            to="/login"
            class="hidden lg:inline-flex text-body-sm text-white/35 hover:text-white/70 transition-colors"
          >
            Sign in
          </NuxtLink>

          <UButton
            label="Sign up"
            to="/signup"
            size="sm"
            class="hidden lg:inline-flex bg-white text-[#0b0d11] hover:bg-white/90 font-semibold rounded-full"
          />

          <!-- Mobile menu button -->
          <UButton
            icon="i-lucide-menu"
            variant="ghost"
            class="lg:hidden text-white/40"
            @click="mobileMenuOpen = !mobileMenuOpen"
          />
        </div>
      </div>

      <!-- Mobile menu -->
      <nav v-if="mobileMenuOpen" class="md:hidden py-4 border-t border-white/[0.04]">
        <div class="flex flex-col gap-3">
          <NuxtLink
            v-for="item in items"
            :key="item.to"
            :to="item.to"
            class="text-body-md text-white/40 hover:text-white/70 py-2"
            @click="mobileMenuOpen = false"
          >
            {{ item.label }}
          </NuxtLink>
          <div class="border-t border-white/[0.04] my-2" />
          <NuxtLink
            to="/login"
            class="text-body-md text-white/40 hover:text-white/70 py-2"
            @click="mobileMenuOpen = false"
          >
            Sign in
          </NuxtLink>
          <UButton
            label="Sign up"
            to="/signup"
            block
            class="bg-white text-[#0b0d11] hover:bg-white/90 font-semibold rounded-full"
            @click="mobileMenuOpen = false"
          />
        </div>
      </nav>
    </div>
  </header>
</template>
