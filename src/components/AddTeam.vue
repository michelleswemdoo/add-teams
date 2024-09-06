<template>
  <div>
    <h1>Add Team</h1>
    <form @submit.prevent="handleSubmit">
      <div class="form-group">
        <input required id="name" type="text" placeholder="Name" v-model="name" />
      </div>

      <!-- :value="name" -->
      <!-- @input="(event) => (name = (event?.target as HTMLInputElement).value)" -->

      <div class="form-group">
        <input required id="email" type="email" placeholder="Email" v-model="email" />
      </div>

      <div class="btn-group">
        <button class="btn-add" type="submit">Add team</button>
      </div>
    </form>
    <p v-if="errorExist">{{ errorExist }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const isNotEmpty = (value: string | number) => value !== ''
const name = ref('')
const email = ref('')
const { errorExist } = defineProps<{ errorExist: string }>()

const emit = defineEmits<{
  (e: 'addTeam', payload: { name: string; email: string }): void
}>()

const handleSubmit = () => {
  if (!isNotEmpty(name.value.trim()) || !isNotEmpty(email.value.trim())) {
    return
  }
  emit('addTeam', { name: name.value, email: email.value })
}
</script>

<style scoped>
h1 {
  font-size: 20px;
  line-height: 28px;
  color: #be185d;
  font-weight: 600;
  margin-bottom: 24px;
  text-align: center;
}

.form-group,
.btn-group {
  margin-bottom: 16px;
}

input,
.btn-add {
  width: 100%;
  padding: 14px 20px;
  border-radius: 4px;
  font-weight: 500;
}
input {
  border-width: 1px;
  background-color: transparent;
  color: inherit;
  font-size: 16px;
}

.btn-add {
  border: none;
  border: 1px solid #be185d;
  background-color: #be185d;
  color: #fff;
  cursor: pointer;
}
</style>
