<template>
  <table>
    <thead>
      <tr>
        <th v-for="(header, index) in tableHeaders" :key="index">{{ header }}</th>
      </tr>
    </thead>
    <tbody>
      <div v-if="teams.length === 0" class="empty-container">
        No teams available. Start adding a team member.
      </div>
      <tr v-else v-for="(team, index) in teams" :key="team.id">
        <td>
          <input type="checkbox" />
        </td>

        <td>
          <p>{{ team.name }}</p>
        </td>

        <td>
          <p>{{ team.email }}</p>
        </td>
        <td>
          <AppButton @click="$emit('removeTeam', index)" variant="secondary" type="button"
            >Remove</AppButton
          >
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup lang="ts">
import AppButton from './ui/AppButton.vue'
import type { Team } from '@/types'
const tableHeaders = ['No', 'Name', 'Email', 'Action']

defineProps<{ teams: Team[] }>()

defineEmits<{ (e: 'removeTeam', index: number): void }>()
</script>

<style scoped>
table {
  width: 100%;
  background-color: #fff;
  border-collapse: collapse;
  border-color: inherit;
  border-radius: 8px;
}

table thead tr th {
  color: #6b7280;
  text-align: left;
  padding: 12px 24px;
  font-size: 14px;
  font-weight: normal;
}

table thead tr {
  border-bottom-width: 2px;
}

table tbody tr {
  border-bottom-width: 1px;
}

table tbody tr td {
  padding: 12px 24px;
}
table tbody tr td p {
  font-size: 14px;
  font-weight: 500;
  text-align: left;
  letter-spacing: 0.025em;
  line-height: 24px;
}
.empty-container {
  text-align: center;
  font-size: 16px;
  font-weight: 500;
  letter-spacing: 0.025em;
  line-height: 26px;
  padding: 12px 24px;
}

input {
  accent-color: #64748b;
}
</style>
