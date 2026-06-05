<template>
  <footer class="border-t border-neutral-200 bg-white">
    <div class="max-w-7xl mx-auto px-6 py-12">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-12">
        <div>
          <h3 class="text-body-sm font-bold text-[#1b1b1b] mb-3">Resources</h3>
          <ul class="space-y-2">
            <li><NuxtLink to="/" class="text-body-sm text-neutral-700 hover:text-blue-50">Help center</NuxtLink></li>
            <li><NuxtLink to="/docs" class="text-body-sm text-neutral-700 hover:text-blue-50">Docs</NuxtLink></li>
            <li><NuxtLink to="/changelog" class="text-body-sm text-neutral-700 hover:text-blue-50">Changelog</NuxtLink></li>
          </ul>
        </div>
        <div>
          <h3 class="text-body-sm font-bold text-[#1b1b1b] mb-3">Features</h3>
          <ul class="space-y-2">
            <li><NuxtLink to="/pricing" class="text-body-sm text-neutral-700 hover:text-blue-50">Pricing</NuxtLink></li>
            <li><NuxtLink to="/" class="text-body-sm text-neutral-700 hover:text-blue-50">Portal</NuxtLink></li>
          </ul>
        </div>
        <div>
          <h3 class="text-body-sm font-bold text-[#1b1b1b] mb-3">Company</h3>
          <ul class="space-y-2">
            <li><NuxtLink to="/" class="text-body-sm text-neutral-700 hover:text-blue-50">About</NuxtLink></li>
            <li><NuxtLink to="/blog" class="text-body-sm text-neutral-700 hover:text-blue-50">Blog</NuxtLink></li>
          </ul>
        </div>
      </div>

      <div class="border-t border-neutral-200 pt-8 flex flex-col md:flex-row items-center justify-between gap-4">
        <p class="text-body-sm text-neutral-600">
          Built with Nuxt UI • © {{ new Date().getFullYear() }}
        </p>
        <div class="flex items-center gap-4">
          <NuxtLink to="/" class="text-body-sm text-neutral-700 hover:text-blue-50">Privacy Policy</NuxtLink>
          <NuxtLink to="/" class="text-body-sm text-neutral-700 hover:text-blue-50">Terms of Service</NuxtLink>
        </div>
      </div>
    </div>
  </footer>
</template>
