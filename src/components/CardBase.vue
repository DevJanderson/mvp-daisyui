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
      <div v-if="avatars.length" class="avatar-group -space-x-6">
        <div v-for="(avatar, index) in avatars" :key="index" class="avatar">
          <div class="w-12">
            <img :src="avatar" />
          </div>
        </div>
      </div>
      <h2 class="card-title">
        {{ title }}
        <div v-if="badge" class="badge badge-secondary">{{ badge }}</div>
      </h2>
      <p>{{ description }}</p>

      <div v-if="tags.length" class="card-actions justify-end">
        <div v-for="tag in tags" :key="tag" class="badge badge-outline">
          {{ tag }}
        </div>
      </div>
    </div>
  </div>
</template>
