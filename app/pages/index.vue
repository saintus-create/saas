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
  <div v-if="page" class="bg-white dark:bg-[#0a0a0a]">
    <!-- Hero Section -->
    <section class="border-b border-neutral-200 dark:border-neutral-800">
      <div class="max-w-5xl mx-auto px-6 py-16">
        <h1 class="text-heading-2xl font-bold text-[#1b1b1b] dark:text-white mb-4 leading-tight">
          {{ page.title }}
        </h1>
        <p class="text-body-lg text-neutral-700 dark:text-neutral-300 mb-8 max-w-3xl">
          {{ page.description }}
        </p>
        <div class="flex flex-wrap gap-3">
          <UButton
            v-for="(link, index) in page.hero.links"
            :key="index"
            v-bind="link"
            :class="index === 0 ? 'bg-blue-50 hover:bg-blue-60 text-white font-semibold' : 'bg-white dark:bg-[#0a0a0a] border-2 border-blue-50 text-blue-50 hover:bg-blue-50 font-semibold'"
          />
        </div>
      </div>
    </section>

    <!-- Features Grid -->
    <section class="border-b border-neutral-200 dark:border-neutral-800 bg-gray-5 dark:bg-[#111111]">
      <div class="max-w-5xl mx-auto px-6 py-16">
        <h2 class="text-heading-xl font-bold text-[#1b1b1b] dark:text-white mb-4">
          {{ page.features.title }}
        </h2>
        <p class="text-body-md text-neutral-700 dark:text-neutral-300 mb-12 max-w-3xl">
          {{ page.features.description }}
        </p>
        
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div
            v-for="(item, index) in page.features.items"
            :key="index"
            class="bg-white dark:bg-[#0a0a0a] border border-neutral-200 dark:border-neutral-800 p-6 hover:border-blue-50 transition-colors"
          >
            <h3 class="text-heading-sm font-bold text-[#1b1b1b] dark:text-white mb-3">
              {{ item.title }}
            </h3>
            <p class="text-body-md text-neutral-700 dark:text-neutral-300 leading-relaxed">
              {{ item.description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Sections -->
    <section
      v-for="(section, index) in page.sections"
      :key="index"
      :class="index % 2 === 0 ? 'bg-white dark:bg-[#0a0a0a]' : 'bg-gray-5 dark:bg-[#111111]'"
      class="border-b border-neutral-200 dark:border-neutral-800"
    >
      <div class="max-w-5xl mx-auto px-6 py-16">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
          <div>
            <h2 class="text-heading-xl font-bold text-[#1b1b1b] dark:text-white mb-4">
              {{ section.title }}
            </h2>
            <p class="text-body-md text-neutral-700 dark:text-neutral-300 leading-relaxed">
              {{ section.description }}
            </p>
          </div>
          
          <div v-if="section.features" class="space-y-6">
            <div
              v-for="(feature, fIndex) in section.features"
              :key="fIndex"
              class="bg-white dark:bg-[#0a0a0a] border border-neutral-200 dark:border-neutral-800 p-5 hover:border-blue-50 transition-colors"
            >
              <h3 class="text-body-lg font-bold text-[#1b1b1b] dark:text-white mb-2">
                {{ feature.name }}
              </h3>
              <p class="text-body-md text-neutral-700 dark:text-neutral-300">
                {{ feature.description }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Testimonials -->
    <section class="border-b border-neutral-200 dark:border-neutral-800">
      <div class="max-w-5xl mx-auto px-6 py-16">
        <h2 class="text-heading-xl font-bold text-[#1b1b1b] dark:text-white mb-4">
          {{ page.testimonials.title }}
        </h2>
        <p class="text-body-md text-neutral-700 dark:text-neutral-300 mb-12">
          {{ page.testimonials.description }}
        </p>
        
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div
            v-for="(testimonial, index) in page.testimonials.items.slice(0, 4)"
            :key="index"
            class="bg-blue-5 dark:bg-blue-900/20 border-l-4 border-blue-50 p-6"
          >
            <blockquote class="text-body-md text-neutral-800 dark:text-neutral-200 mb-4 leading-relaxed italic">
              "{{ testimonial.quote }}"
            </blockquote>
            <div class="border-t border-blue-20 dark:border-blue-800 pt-4">
              <cite class="text-body-sm font-bold text-[#1b1b1b] dark:text-white not-italic">
                {{ testimonial.user.name }}
              </cite>
              <p class="text-body-xs text-neutral-600 dark:text-neutral-400">
                {{ testimonial.user.description }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA -->
    <section>
      <div class="max-w-5xl mx-auto px-6 py-16">
        <h2 class="text-heading-xl font-bold text-[#1b1b1b] dark:text-white mb-4">
          {{ page.cta.title }}
        </h2>
        <p class="text-body-md text-neutral-700 dark:text-neutral-300 mb-8">
          {{ page.cta.description }}
        </p>
        <div class="flex flex-wrap gap-3">
          <UButton
            v-for="(link, index) in page.cta.links"
            :key="index"
            v-bind="link"
            :class="index === 0 ? 'bg-blue-50 hover:bg-blue-60 text-white font-semibold' : 'bg-white dark:bg-[#0a0a0a] border-2 border-blue-50 text-blue-50 hover:bg-blue-50 font-semibold'"
          />
        </div>
      </div>
    </section>
  </div>
</template>
