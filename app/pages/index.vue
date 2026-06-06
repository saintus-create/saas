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

// Slide deck state
const currentSlide = ref(0)
const totalSlides = 7
const deckRef = ref<HTMLElement | null>(null)

const slides = computed(() => {
  if (!page.value) return []
  return [
    { id: 'hero', label: 'Home' },
    { id: 'features', label: 'Features' },
    { id: 'banner', label: 'Overview' },
    { id: 'platform', label: 'Platform' },
    { id: 'showcase', label: 'Showcase' },
    { id: 'whatsnew', label: 'Updates' },
    { id: 'cta', label: 'Get Started' }
  ]
})

function goToSlide(index: number) {
  if (!deckRef.value) return
  const slideWidth = deckRef.value.clientWidth
  deckRef.value.scrollTo({
    left: slideWidth * index,
    behavior: 'smooth'
  })
}

function nextSlide() {
  if (currentSlide.value < totalSlides - 1) {
    goToSlide(currentSlide.value + 1)
  }
}

function prevSlide() {
  if (currentSlide.value > 0) {
    goToSlide(currentSlide.value - 1)
  }
}

// Track active slide via scroll position
function onScroll() {
  if (!deckRef.value) return
  const slideWidth = deckRef.value.clientWidth
  const scrollLeft = deckRef.value.scrollLeft
  currentSlide.value = Math.round(scrollLeft / slideWidth)
}

// Keyboard navigation
function onKeyDown(e: KeyboardEvent) {
  if (e.key === 'ArrowRight' || e.key === 'ArrowDown') {
    e.preventDefault()
    nextSlide()
  } else if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') {
    e.preventDefault()
    prevSlide()
  }
}

onMounted(() => {
  window.addEventListener('keydown', onKeyDown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', onKeyDown)
})
</script>

<template>
  <div v-if="page" class="bg-[#0b0d11] text-white antialiased h-screen overflow-hidden">

    <!-- Slide Deck Container -->
    <div
      ref="deckRef"
      class="slide-deck flex h-full overflow-x-auto overflow-y-hidden touch-pan-x"
      @scroll="onScroll"
    >
      <!-- Slide 1: Hero -->
      <section class="slide min-w-full h-full flex-shrink-0 flex flex-col overflow-hidden touch-pan-x">
        <div class="flex-1 flex items-center justify-center relative py-8">
        <div class="absolute top-0 left-1/2 -translate-x-1/2 -translate-y-1/3 w-[500px] h-[500px] bg-white/[0.02] rounded-full blur-3xl pointer-events-none" />
        <div class="max-w-3xl mx-auto px-6 sm:px-8 text-center relative">
          <div class="w-14 h-14 rounded-full border border-white/[0.10] flex items-center justify-center mx-auto mb-8">
            <UIcon :name="page.hero.icon" class="w-8 h-8 text-white/50" />
          </div>
          <h1 class="text-heading-lg sm:text-heading-xl font-bold tracking-tight leading-[1.08] mb-6">
            {{ page.hero.title }}
          </h1>
          <p class="text-body-lg sm:text-body-xl text-white/50 max-w-lg mx-auto mb-10 leading-[1.7]">
            {{ page.hero.subtitle }}
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <UButton
              v-bind="page.hero.cta.primary"
              size="xl"
              class="bg-white text-[#0b0d11] hover:bg-white/90 font-semibold rounded-full min-h-[52px] text-body-lg"
            />
            <UButton
              v-bind="page.hero.cta.secondary"
              size="xl"
              variant="ghost"
              class="text-white/50 hover:text-white/80 rounded-full min-h-[52px]"
            />
          </div>
        </div>
        </div>
      </section>

      <!-- Slide 2: 2x2 Feature Grid -->
      <section class="slide min-w-full h-full flex-shrink-0 flex flex-col overflow-hidden touch-pan-x">
        <div class="flex-1 flex items-center justify-center py-8">
          <div class="max-w-5xl mx-auto px-6 w-full">
          <h2 class="text-heading-lg font-bold tracking-tight leading-[1.08] mb-4 text-center">
            {{ page.featureGrid.title }}
          </h2>
          <p class="text-body-lg text-white/40 max-w-lg mx-auto text-center mb-8 leading-[1.7]">
            {{ page.featureGrid.description }}
          </p>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-px bg-white/[0.08] rounded-[var(--radius-x04)] overflow-hidden">
            <div
              v-for="(item, index) in page.featureGrid.items"
              :key="index"
              class="bg-[#0b0d11] p-6 sm:p-8"
            >
              <UIcon :name="item.icon" class="w-8 h-8 text-white/30 mb-4" />
              <h3 class="text-heading-xs font-bold tracking-tight leading-[1.08] mb-2 text-white/90">
                {{ item.title }}
              </h3>
              <p class="text-body-lg text-white/40 leading-[1.7]">
                {{ item.description }}
              </p>
            </div>
          </div>
          </div>
        </div>
      </section>

      <!-- Slide 3: Banner -->
      <section class="slide min-w-full h-full flex-shrink-0 flex flex-col overflow-hidden touch-pan-x">
        <div class="flex-1 flex items-center justify-center py-8">
          <div class="max-w-3xl mx-auto px-6 text-center">
          <h2 class="text-heading-lg sm:text-heading-xl font-bold tracking-tight leading-[1.08] mb-6">
            {{ page.banner.title }}
          </h2>
          <p class="text-body-lg sm:text-body-xl text-white/40 leading-[1.7] max-w-xl mx-auto">
            {{ page.banner.subtitle }}
          </p>
          </div>
        </div>
      </section>

      <!-- Slide 4: Platform / Tools -->
      <section class="slide min-w-full h-full flex-shrink-0 flex flex-col overflow-hidden touch-pan-x">
        <div class="flex-1 flex items-center justify-center py-8">
          <div class="max-w-5xl mx-auto px-6 text-center w-full">
          <h2 class="text-heading-md font-bold tracking-tight leading-[1.08] mb-4">
            {{ page.platform.title }}
          </h2>
          <p class="text-body-lg text-white/40 max-w-lg mx-auto mb-10 leading-[1.7]">
            {{ page.platform.description }}
          </p>
          <div class="grid grid-cols-2 sm:grid-cols-4 gap-6 sm:gap-10">
            <div
              v-for="(tool, index) in page.platform.tools"
              :key="index"
              class="flex flex-col items-center gap-3"
            >
              <div class="w-14 h-14 rounded-[var(--radius-x03)] border border-white/[0.08] flex items-center justify-center">
                <UIcon :name="tool.icon" class="w-6 h-6 text-white/35" />
              </div>
              <span class="text-body-md text-white/35">{{ tool.label }}</span>
            </div>
          </div>
          </div>
        </div>
      </section>

      <!-- Slide 5: Showcase Grid -->
      <section class="slide min-w-full h-full flex-shrink-0 flex flex-col overflow-hidden touch-pan-x">
        <div class="flex-1 flex items-center justify-center py-8">
          <div class="max-w-5xl mx-auto px-6 w-full">
          <h2 class="text-heading-lg font-bold tracking-tight leading-[1.08] mb-4 text-center">
            {{ page.showcase.title }}
          </h2>
          <p class="text-body-lg text-white/40 max-w-lg mx-auto text-center mb-8 leading-[1.7]">
            {{ page.showcase.description }}
          </p>
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-px bg-white/[0.08] rounded-[var(--radius-x04)] overflow-hidden">
            <div
              v-for="(item, index) in page.showcase.items"
              :key="index"
              class="bg-[#0b0d11] p-6"
            >
              <div class="w-10 h-10 rounded-[var(--radius-x02)] border border-white/[0.08] flex items-center justify-center mb-4">
                <UIcon :name="item.icon" class="w-5 h-5 text-white/30" />
              </div>
              <h3 class="text-heading-xs font-bold tracking-tight leading-[1.08] mb-2 text-white/90">
                {{ item.title }}
              </h3>
              <p class="text-body-lg text-white/40 leading-[1.7]">
                {{ item.description }}
              </p>
            </div>
          </div>
          </div>
        </div>
      </section>

      <!-- Slide 6: What's New -->
      <section class="slide min-w-full h-full flex-shrink-0 flex flex-col overflow-hidden touch-pan-x">
        <div class="flex-1 flex items-center justify-center py-8">
          <div class="max-w-4xl mx-auto px-6 w-full">
          <h2 class="text-heading-lg font-bold tracking-tight leading-[1.08] mb-4 text-center">
            {{ page.whatsNew.title }}
          </h2>
          <p class="text-body-lg text-white/40 max-w-lg mx-auto text-center mb-8 leading-[1.7]">
            {{ page.whatsNew.description }}
          </p>
          <div class="grid grid-cols-1 gap-px bg-white/[0.08] rounded-[var(--radius-x04)] overflow-hidden">
            <div
              v-for="(item, index) in page.whatsNew.items"
              :key="index"
              class="bg-[#0b0d11] p-6"
            >
              <span class="text-body-md text-white/25 mb-2 block">{{ item.date }}</span>
              <h3 class="text-heading-xs font-bold tracking-tight leading-[1.08] mb-2 text-white/85">
                {{ item.title }}
              </h3>
              <p class="text-body-lg text-white/40 leading-[1.7]">
                {{ item.description }}
              </p>
            </div>
          </div>
          </div>
        </div>
      </section>

      <!-- Slide 7: CTA + Footer -->
      <section class="slide min-w-full h-full flex-shrink-0 flex flex-col overflow-hidden touch-pan-x">
        <div class="flex-1 flex items-center justify-center py-8">
          <div class="max-w-3xl mx-auto px-6 text-center w-full">
          <h2 class="text-heading-lg sm:text-heading-xl font-bold tracking-tight leading-[1.08] mb-4">
            {{ page.cta.title }}
          </h2>
          <p class="text-body-lg sm:text-body-xl text-white/40 mb-10 max-w-lg mx-auto leading-[1.7]">
            {{ page.cta.description }}
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center mb-16">
            <UButton
              v-for="(link, index) in page.cta.links"
              :key="index"
              v-bind="link"
              size="xl"
              :class="index === 0 ? 'bg-white text-[#0b0d11] hover:bg-white/90 font-semibold rounded-full min-h-[52px] text-body-lg' : 'text-white/50 hover:text-white/80 rounded-full min-h-[52px]'"
            />
          </div>
          <!-- Inline footer links -->
          <div class="flex flex-wrap justify-center gap-6">
            <NuxtLink
              v-for="(link, lIndex) in page.resourceFooter.columns[0]?.links"
              :key="lIndex"
              :to="link.to"
              :target="link.target"
              class="text-body-md text-white/25 hover:text-white/50 transition-colors"
            >
              {{ link.label }}
            </NuxtLink>
          </div>
        </div>
        </div>
      </section>
    </div>

    <!-- Dot Indicator - Fixed at bottom -->
    <div class="fixed bottom-8 left-1/2 -translate-x-1/2 z-50">
      <div class="flex items-center gap-2 bg-white/[0.06] backdrop-blur-md rounded-full px-4 py-2.5 border border-white/[0.06]">
        <button
          v-for="(slide, index) in slides"
          :key="index"
          class="w-2 h-2 rounded-full transition-all duration-300"
          :class="currentSlide === index ? 'bg-white scale-125' : 'bg-white/25 hover:bg-white/40'"
          :aria-label="`Go to ${slide.label}`"
          @click="goToSlide(index)"
        />
      </div>
    </div>

    <!-- Arrow Navigation (desktop) -->
    <button
      v-if="currentSlide > 0"
      class="fixed left-4 top-1/2 -translate-y-1/2 z-50 w-10 h-10 rounded-full bg-white/[0.06] backdrop-blur-md border border-white/[0.06] flex items-center justify-center text-white/40 hover:text-white/70 transition-colors"
      aria-label="Previous slide"
      @click="prevSlide()"
    >
      <UIcon name="i-lucide-chevron-left" class="w-5 h-5" />
    </button>
    <button
      v-if="currentSlide < totalSlides - 1"
      class="fixed right-4 top-1/2 -translate-y-1/2 z-50 w-10 h-10 rounded-full bg-white/[0.06] backdrop-blur-md border border-white/[0.06] flex items-center justify-center text-white/40 hover:text-white/70 transition-colors"
      aria-label="Next slide"
      @click="nextSlide()"
    >
      <UIcon name="i-lucide-chevron-right" class="w-5 h-5" />
    </button>
  </div>
</template>
