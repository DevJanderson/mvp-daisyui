<script setup>
defineProps({
  size: {
    type: String,
    default: 'loading-md',
    validator: (value) => ['loading-xs', 'loading-sm', 'loading-md', 'loading-lg'].includes(value),
  },
  variant: {
    type: String,
    default: 'loading-spinner',
    validator: (value) =>
      ['loading-spinner', 'loading-dots', 'loading-ring', 'loading-ball', 'loading-bars', 'loading-infinity'].includes(value),
  },
})
</script>

<template>
  <div class="flex justify-center">
    <span class="loading" :class="[variant, size]">
      <slot />
    </span>
  </div>
</template>
