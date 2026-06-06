<script setup lang="ts">
defineProps<{
  icon: string
  title: string
  description: string
  accent?: string
}>()
</script>

<template>
  <div class="bg-gray-100 rounded-[var(--radius-x04)] p-8 border-t-2 border-blue-60 hover:border-blue-50 transition-colors">
    <UIcon :name="icon" class="w-10 h-10 text-blue-50 mb-4" />
    <h3 class="text-heading-xs font-bold text-white mb-3 tracking-tight">
      {{ title }}
    </h3>
    <p class="text-body-lg text-gray-40 leading-relaxed">
      {{ description }}
    </p>
  </div>
</template>
