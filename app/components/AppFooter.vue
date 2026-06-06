<template>
  <footer class="border-t border-white/[0.04] bg-[#0b0d11]">
    <div class="max-w-5xl mx-auto px-6 py-16">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-10 mb-14">
        <div>
          <h3 class="text-body-sm font-semibold text-white/50 mb-4 tracking-tight">Resources</h3>
          <ul class="space-y-3">
            <li><NuxtLink to="/" class="text-body-md text-white/25 hover:text-white/50 transition-colors leading-[1.7]">Help center</NuxtLink></li>
            <li><NuxtLink to="/docs" class="text-body-md text-white/25 hover:text-white/50 transition-colors leading-[1.7]">Docs</NuxtLink></li>
            <li><NuxtLink to="/changelog" class="text-body-md text-white/25 hover:text-white/50 transition-colors leading-[1.7]">Changelog</NuxtLink></li>
          </ul>
        </div>
        <div>
          <h3 class="text-body-sm font-semibold text-white/50 mb-4 tracking-tight">Features</h3>
          <ul class="space-y-3">
            <li><NuxtLink to="/pricing" class="text-body-md text-white/25 hover:text-white/50 transition-colors leading-[1.7]">Pricing</NuxtLink></li>
            <li><NuxtLink to="/" class="text-body-md text-white/25 hover:text-white/50 transition-colors leading-[1.7]">Portal</NuxtLink></li>
          </ul>
        </div>
        <div>
          <h3 class="text-body-sm font-semibold text-white/50 mb-4 tracking-tight">Company</h3>
          <ul class="space-y-3">
            <li><NuxtLink to="/" class="text-body-md text-white/25 hover:text-white/50 transition-colors leading-[1.7]">About</NuxtLink></li>
            <li><NuxtLink to="/blog" class="text-body-md text-white/25 hover:text-white/50 transition-colors leading-[1.7]">Blog</NuxtLink></li>
          </ul>
        </div>
      </div>

      <div class="border-t border-white/[0.04] pt-8 flex flex-col md:flex-row items-center justify-between gap-4">
        <p class="text-body-sm text-white/20">
          Built with Nuxt UI &bull; {{ new Date().getFullYear() }}
        </p>
        <div class="flex items-center gap-6">
          <NuxtLink to="/" class="text-body-sm text-white/25 hover:text-white/50 transition-colors">Privacy Policy</NuxtLink>
          <NuxtLink to="/" class="text-body-sm text-white/25 hover:text-white/50 transition-colors">Terms of Service</NuxtLink>
        </div>
      </div>
    </div>
  </footer>
</template>
