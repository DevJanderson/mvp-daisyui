<script setup>
defineProps({
  src: {
    type: String,
    required: true,
  },
  name: {
    type: String,
    default: '',
  },
  size: {
    type: String,
    default: 'w-16',
  },
  rounded: {
    type: Boolean,
    default: true,
  },
})
</script>

<template>
  <div class="flex flex-col items-center text-center">
    <div class="avatar">
      <div :class="[size, { 'rounded-full': rounded }]">
        <img :src="src" :alt="name" />
      </div>
    </div>
    <slot>
      <span v-if="name" class="text-xs mt-1">{{ name }}</span>
    </slot>
  </div>
</template>
