<script setup>
const text = ref('')
</script>

<template>
  <DefaultLayout>
    <div class="container mx-auto p-4">
      <input v-model="text" type="text" placeholder="Type here" class="input" />
      {{ text }}
    </div>
  </DefaultLayout>
</template>
