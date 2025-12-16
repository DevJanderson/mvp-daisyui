<script setup>
const props = defineProps({
  id: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    default: '',
  },
})

function open() {
  document.getElementById(props.id).showModal()
}

function close() {
  document.getElementById(props.id).close()
}

defineExpose({ open, close })
</script>

<template>
  <dialog :id="id" class="modal">
    <div class="modal-box">
      <h3 v-if="title" class="text-lg font-bold">{{ title }}</h3>
      <div class="py-4">
        <slot />
      </div>
      <div class="modal-action">
        <form method="dialog">
          <button class="btn">Fechar</button>
        </form>
      </div>
    </div>
    <form method="dialog" class="modal-backdrop">
      <button>close</button>
    </form>
  </dialog>
</template>
