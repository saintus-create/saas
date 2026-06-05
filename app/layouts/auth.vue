<template>
  <div class="min-h-screen flex flex-col bg-[#f0f0f0] dark:bg-neutral-950">
    <!-- USWDS Official Government Banner -->
    <div class="bg-[#f0f0f0] dark:bg-neutral-800 border-b border-[#dfe1e2] dark:border-neutral-700">
      <div class="max-w-7xl mx-auto px-4 py-1 flex items-center gap-2">
        <svg class="w-4 h-4 shrink-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 491.522 491.522">
          <path fill="#BF0A30" d="M0 0h491.522v37.808H0z"/>
          <path fill="#FFFFFF" d="M0 37.808h491.522v37.808H0z"/>
          <path fill="#002868" d="M0 75.616h245.761v75.616H0z"/>
          <path fill="#BF0A30" d="M0 113.425h491.522v37.808H0z"/>
          <path fill="#FFFFFF" d="M245.761 75.616h245.761v37.808H245.761z"/>
          <path fill="#BF0A30" d="M0 151.233h491.522v37.808H0z"/>
          <path fill="#FFFFFF" d="M0 189.041h491.522v37.808H0z"/>
        </svg>
        <p class="text-xs text-[#1b1b1b] dark:text-neutral-300">
          An official website of the United States government
        </p>
      </div>
    </div>

    <!-- USWDS Site Header -->
    <header class="bg-[#162e51] text-white">
      <div class="max-w-7xl mx-auto px-4 py-4 flex items-center justify-between">
        <NuxtLink to="/" class="flex items-center gap-3 hover:opacity-90 transition-opacity">
          <AppLogo class="h-8 w-auto text-white" />
        </NuxtLink>
        <nav class="hidden sm:flex items-center gap-6 text-sm text-blue-200">
          <NuxtLink to="/docs" class="hover:text-white transition-colors">Docs</NuxtLink>
          <NuxtLink to="/pricing" class="hover:text-white transition-colors">Pricing</NuxtLink>
          <NuxtLink to="/blog" class="hover:text-white transition-colors">Blog</NuxtLink>
          <NuxtLink to="/changelog" class="hover:text-white transition-colors">Changelog</NuxtLink>
        </nav>
        <div class="text-right text-xs text-blue-200">
          <p class="font-semibold">Agency Contact Center</p>
          <p>(800) 555-0100 • Mon–Fri 8am–6pm ET</p>
        </div>
      </div>
    </header>

    <!-- Page Content -->
    <main class="flex-1 py-10">
      <div class="max-w-7xl mx-auto px-4">
        <div class="bg-white dark:bg-neutral-900 border-l-4 border-[#005ea2] shadow-sm">
          <div class="p-8 lg:p-12">
            <slot />
          </div>
        </div>
      </div>
    </main>

    <!-- USWDS Footer -->
    <footer class="bg-[#162e51] text-white mt-auto">
      <div class="max-w-7xl mx-auto px-4 py-8 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
        <div>
          <AppLogo class="h-6 w-auto text-white mb-2" />
          <p class="text-xs text-blue-200">An official website of the U.S. government</p>
        </div>
        <nav class="flex gap-4 text-xs text-blue-200 flex-wrap">
          <NuxtLink to="/" class="hover:text-white transition-colors">Contact</NuxtLink>
          <NuxtLink to="/" class="hover:text-white transition-colors">Policies</NuxtLink>
          <NuxtLink to="/" class="hover:text-white transition-colors">Getting started</NuxtLink>
          <NuxtLink to="/" class="hover:text-white transition-colors">About us</NuxtLink>
        </nav>
      </div>
    </footer>
  </div>
</template>
