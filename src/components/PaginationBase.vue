<script setup>
defineProps({
  totalPages: {
    type: Number,
    required: true,
  },
  currentPage: {
    type: Number,
    default: 1,
  },
})

const emit = defineEmits(['update:currentPage'])

function goToPage(page) {
  emit('update:currentPage', page)
}
</script>

<template>
  <div class="flex justify-center mt-4">
    <div class="join">
      <slot name="prev">
        <button
          class="join-item btn"
          :disabled="currentPage === 1"
          @click="goToPage(currentPage - 1)"
        >
          «
        </button>
      </slot>

      <button
        v-for="page in totalPages"
        :key="page"
        class="join-item btn"
        :class="{ 'btn-active': page === currentPage }"
        @click="goToPage(page)"
      >
        <slot name="page" :page="page">
          {{ page }}
        </slot>
      </button>

      <slot name="next">
        <button
          class="join-item btn"
          :disabled="currentPage === totalPages"
          @click="goToPage(currentPage + 1)"
        >
          »
        </button>
      </slot>
    </div>
  </div>
</template>
