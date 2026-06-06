<script setup lang="ts">
defineProps<{
  variant?: 'dark' | 'darker' | 'gradient'
  padding?: 'sm' | 'md' | 'lg'
}>()
</script>

<template>
  <section
    class="w-full"
    :class="[
      variant === 'gradient' ? 'gradient-navy' : variant === 'darker' ? 'bg-gray-100' : 'bg-gray-90',
      padding === 'sm' ? 'py-12' : padding === 'lg' ? 'py-24' : 'py-16'
    ]"
  >
    <div class="max-w-7xl mx-auto px-6">
      <slot />
    </div>
  </section>
</template>
