<template>
  <button :class="computedClasses" :type="type" :disabled="disabled" @click="onClick">
    <slot />
  </button>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const { disabled, variant } = defineProps<{
  variant?: 'primary' | 'secondary'
  type?: 'submit' | 'button'
  disabled?: boolean
}>()

const emit = defineEmits(['click'])

const computedClasses = computed(() => {
  return ['btn', `btn--${variant}`].join(' ')
})

const onClick = () => {
  if (!disabled) {
    emit('click')
  }
}
</script>

<style scoped>
.btn {
  border: none;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  border-radius: 6px;
}

.btn--primary {
  border: 1px solid #be185d;
  background-color: #be185d;
  padding: 8px 24px;
  color: #fff;
}

.btn--secondary {
  border: 1px solid rgba(190, 24, 93, 0.15);
  background-color: rgba(190, 24, 93, 0.15);
  padding: 4px 12px;
  color: #be185d;
}
</style>
