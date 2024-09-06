<template>
  <teleport to="body">
    <div v-if="isOpen" @click="$emit('onClose')" class="modal-overlay">
      <div @click.stop class="modal-content">
        <button @click="$emit('onClose')">X</button>
        <slot />
      </div>
    </div>
  </teleport>
</template>

<script setup lang="ts">
defineProps<{ isOpen: boolean }>()
defineEmits(['onClose'])
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  height: 100dvh;
  inset: 0;
  z-index: 9999;
  background: rgba(0, 0, 0, 0.35);
  padding: 0;
}

.modal-content {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  border-radius: 8px;
  padding: 32px;
  width: 100%;
  max-width: 560px;
}

button {
  font-size: 18px;
  font-weight: 500;
  position: absolute;
  top: 12.8px;
  right: 12.8px;
  color: #be185d;
  border: none;
  border: 1px solid transparent;
  cursor: pointer;
  background: transparent;
}
</style>
