<script setup>
defineProps({
  avatars: {
    type: Array,
    default: () => [],
  },
  size: {
    type: String,
    default: 'w-12',
  },
  max: {
    type: Number,
    default: 0,
  },
})
</script>

<template>
  <div class="avatar-group -space-x-6">
    <div
      v-for="(avatar, index) in max ? avatars.slice(0, max) : avatars"
      :key="index"
      class="avatar"
    >
      <div :class="size">
        <slot name="avatar" :avatar="avatar" :index="index">
          <img :src="avatar" />
        </slot>
      </div>
    </div>

    <!-- Slot para mostrar contador de extras -->
    <slot name="extra" :remaining="max && avatars.length > max ? avatars.length - max : 0">
      <div v-if="max && avatars.length > max" class="avatar placeholder">
        <div :class="[size, 'bg-neutral text-neutral-content']">
          <span>+{{ avatars.length - max }}</span>
        </div>
      </div>
    </slot>
  </div>
</template>
