<script setup>
defineProps({
  variant: {
    type: String,
    default: 'badge-outline',
  },
})
</script>

<template>
  <div class="badge" :class="variant">
    <slot />
  </div>
</template>
