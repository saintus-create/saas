<script setup lang="ts">
defineProps<{
  icon: string
  title: string
  description: string
}>()
</script>

<template>
  <div class="bg-white rounded-[var(--radius-x04)] p-6 shadow-3xl hover:shadow-lg transition-shadow border border-gray-20">
    <div class="w-12 h-12 rounded-[var(--radius-x03)] bg-blue-60/10 flex items-center justify-center mb-4">
      <UIcon :name="icon" class="w-6 h-6 text-blue-60" />
    </div>
    <h3 class="text-heading-xs font-bold text-gray-100 mb-2 tracking-tight">
      {{ title }}
    </h3>
    <p class="text-body-md text-gray-60 leading-relaxed">
      {{ description }}
    </p>
  </div>
</template>
