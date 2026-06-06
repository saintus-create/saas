<script setup lang="ts">
defineProps<{
  variant?: 'white' | 'gray'
  padding?: 'sm' | 'md' | 'lg'
}>()
</script>

<template>
  <section
    class="w-full"
    :class="[
      variant === 'gray' ? 'bg-gray-10' : 'bg-gray-0',
      padding === 'sm' ? 'py-12' : padding === 'lg' ? 'py-24' : 'py-16'
    ]"
  >
    <div class="max-w-7xl mx-auto px-6">
      <slot />
    </div>
  </section>
</template>
