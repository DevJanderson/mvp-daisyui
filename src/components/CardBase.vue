<script setup>
defineProps({
  title: {
    type: String,
    default: '',
  },
  description: {
    type: String,
    default: '',
  },
  avatars: {
    type: Array,
    default: () => [],
  },
  badge: {
    type: String,
    default: '',
  },
  tags: {
    type: Array,
    default: () => [],
  },
})
</script>

<template>
  <div class="card bg-base-100 w-96 shadow-sm mb-1">
    <div class="card-body">
      <slot name="header">
        <AvatarGroup v-if="avatars.length" :avatars="avatars" />
      </slot>

      <h2 class="card-title">
        {{ title }}
        <BadgeBase v-if="badge" variant="badge-secondary">{{ badge }}</BadgeBase>
      </h2>

      <slot>
        <p>{{ description }}</p>
      </slot>

      <div v-if="tags.length" class="card-actions justify-end">
        <BadgeBase v-for="tag in tags" :key="tag">{{ tag }}</BadgeBase>
      </div>

      <slot name="footer" />
    </div>
  </div>
</template>
