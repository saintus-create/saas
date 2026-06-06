<script setup lang="ts">
const { data: page } = await useAsyncData('index', () => queryCollection('index').first())

const title = page.value?.seo?.title || page.value?.title
const description = page.value?.seo?.description || page.value?.description

useSeoMeta({
  titleTemplate: '',
  title,
  ogTitle: title,
  description,
  ogDescription: description,
  ogImage: 'https://ui.nuxt.com/assets/templates/nuxt/saas-light.png'
})
</script>

<template>
  <div v-if="page" class="bg-[#0b0d11] text-white antialiased">

    <!-- Hero -->
    <section class="relative pt-32 pb-28">
      <div class="absolute top-0 left-1/2 -translate-x-1/2 -translate-y-1/3 w-[500px] h-[500px] bg-white/[0.02] rounded-full blur-3xl pointer-events-none" />
      <div class="max-w-3xl mx-auto px-6 text-center relative">
        <div class="w-14 h-14 rounded-full border border-white/[0.08] flex items-center justify-center mx-auto mb-10">
          <UIcon :name="page.hero.icon" class="w-7 h-7 text-white/40" />
        </div>
        <h1 class="text-heading-xl font-bold tracking-tight leading-[1.08] mb-6">
          {{ page.hero.title }}
        </h1>
        <p class="text-body-xl text-white/40 max-w-lg mx-auto mb-10 leading-[1.7]">
          {{ page.hero.subtitle }}
        </p>
        <div class="flex flex-wrap gap-3 justify-center">
          <UButton
            v-bind="page.hero.cta.primary"
            size="xl"
            class="bg-white text-[#0b0d11] hover:bg-white/90 font-semibold rounded-full"
          />
          <UButton
            v-bind="page.hero.cta.secondary"
            size="xl"
            variant="ghost"
            class="text-white/40 hover:text-white/70 rounded-full"
          />
        </div>
      </div>
    </section>

    <!-- 2x2 Feature Grid -->
    <section class="py-24">
      <div class="max-w-5xl mx-auto px-6">
        <h2 class="text-heading-lg font-bold tracking-tight leading-[1.08] mb-4 text-center">
          {{ page.featureGrid.title }}
        </h2>
        <p class="text-body-lg text-white/35 max-w-lg mx-auto text-center mb-16 leading-[1.7]">
          {{ page.featureGrid.description }}
        </p>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-px bg-white/[0.06] rounded-[var(--radius-x04)] overflow-hidden">
          <div
            v-for="(item, index) in page.featureGrid.items"
            :key="index"
            class="bg-[#0b0d11] p-10"
          >
            <UIcon :name="item.icon" class="w-8 h-8 text-white/25 mb-5" />
            <h3 class="text-heading-xs font-bold tracking-tight leading-[1.08] mb-3 text-white/90">
              {{ item.title }}
            </h3>
            <p class="text-body-md text-white/35 leading-[1.7]">
              {{ item.description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Banner -->
    <section class="py-24">
      <div class="max-w-3xl mx-auto px-6 text-center">
        <h2 class="text-heading-lg font-bold tracking-tight leading-[1.08] mb-6">
          {{ page.banner.title }}
        </h2>
        <p class="text-body-xl text-white/35 leading-[1.7] max-w-xl mx-auto">
          {{ page.banner.subtitle }}
        </p>
      </div>
    </section>

    <!-- Platform / Tools -->
    <section class="py-24">
      <div class="max-w-5xl mx-auto px-6 text-center">
        <h2 class="text-heading-md font-bold tracking-tight leading-[1.08] mb-4">
          {{ page.platform.title }}
        </h2>
        <p class="text-body-lg text-white/35 max-w-lg mx-auto mb-14 leading-[1.7]">
          {{ page.platform.description }}
        </p>
        <div class="flex flex-wrap justify-center gap-10">
          <div
            v-for="(tool, index) in page.platform.tools"
            :key="index"
            class="flex flex-col items-center gap-2.5"
          >
            <div class="w-12 h-12 rounded-[var(--radius-x03)] border border-white/[0.06] flex items-center justify-center">
              <UIcon :name="tool.icon" class="w-5 h-5 text-white/30" />
            </div>
            <span class="text-body-sm text-white/25">{{ tool.label }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Showcase Grid -->
    <section class="py-24">
      <div class="max-w-5xl mx-auto px-6">
        <h2 class="text-heading-lg font-bold tracking-tight leading-[1.08] mb-4 text-center">
          {{ page.showcase.title }}
        </h2>
        <p class="text-body-lg text-white/35 max-w-lg mx-auto text-center mb-16 leading-[1.7]">
          {{ page.showcase.description }}
        </p>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-px bg-white/[0.06] rounded-[var(--radius-x04)] overflow-hidden">
          <div
            v-for="(item, index) in page.showcase.items"
            :key="index"
            class="bg-[#0b0d11] p-8"
          >
            <div class="w-10 h-10 rounded-[var(--radius-x02)] border border-white/[0.06] flex items-center justify-center mb-5">
              <UIcon :name="item.icon" class="w-5 h-5 text-white/25" />
            </div>
            <h3 class="text-heading-xs font-bold tracking-tight leading-[1.08] mb-2 text-white/90">
              {{ item.title }}
            </h3>
            <p class="text-body-md text-white/30 leading-[1.7]">
              {{ item.description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- What's New -->
    <section class="py-24">
      <div class="max-w-4xl mx-auto px-6">
        <h2 class="text-heading-lg font-bold tracking-tight leading-[1.08] mb-4 text-center">
          {{ page.whatsNew.title }}
        </h2>
        <p class="text-body-lg text-white/35 max-w-lg mx-auto text-center mb-16 leading-[1.7]">
          {{ page.whatsNew.description }}
        </p>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-px bg-white/[0.06] rounded-[var(--radius-x04)] overflow-hidden">
          <div
            v-for="(item, index) in page.whatsNew.items"
            :key="index"
            class="bg-[#0b0d11] p-8"
          >
            <span class="text-body-sm text-white/20 mb-2 block">{{ item.date }}</span>
            <h3 class="text-heading-xs font-bold tracking-tight leading-[1.08] mb-2 text-white/80">
              {{ item.title }}
            </h3>
            <p class="text-body-md text-white/30 leading-[1.7]">
              {{ item.description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA -->
    <section class="py-28">
      <div class="max-w-3xl mx-auto px-6 text-center">
        <h2 class="text-heading-lg font-bold tracking-tight leading-[1.08] mb-4">
          {{ page.cta.title }}
        </h2>
        <p class="text-body-xl text-white/35 mb-10 max-w-lg mx-auto leading-[1.7]">
          {{ page.cta.description }}
        </p>
        <div class="flex flex-wrap gap-3 justify-center">
          <UButton
            v-for="(link, index) in page.cta.links"
            :key="index"
            v-bind="link"
            size="xl"
            :class="index === 0 ? 'bg-white text-[#0b0d11] hover:bg-white/90 font-semibold rounded-full' : 'text-white/40 hover:text-white/70 rounded-full'"
          />
        </div>
      </div>
    </section>

    <!-- Resource Footer -->
    <footer class="py-20 border-t border-white/[0.04]">
      <div class="max-w-5xl mx-auto px-6">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-10">
          <div
            v-for="(column, index) in page.resourceFooter.columns"
            :key="index"
          >
            <div class="flex items-center gap-2 mb-5">
              <UIcon :name="column.icon" class="w-4 h-4 text-white/20" />
              <span class="text-body-sm font-semibold text-white/50 tracking-tight">{{ column.title }}</span>
            </div>
            <ul class="space-y-3">
              <li v-for="(link, lIndex) in column.links" :key="lIndex">
                <NuxtLink
                  :to="link.to"
                  :target="link.target"
                  class="text-body-md text-white/25 hover:text-white/50 transition-colors leading-[1.7]"
                >
                  {{ link.label }}
                </NuxtLink>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>
