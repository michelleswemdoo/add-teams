<template>
  <APPModal :isOpen="isOpen" @onClose="closeModal">
    <AddTeam @addTeam="addTeam" :errorExist="errorExist" />
  </APPModal>
  <AppLayout>
    <div class="app-container">
      <div class="header-box">
        <h1>Teams</h1>
        <AppButton variant="primary" type="button" @click="openModal">Add Team</AppButton>
      </div>
      <TheTeams :teams="teams" @removeTeam="removeTeam" />
    </div>
  </AppLayout>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import AddTeam from './AddTeam.vue'
import AppLayout from './layout/AppLayout.vue'
import TheTeams from './TheTeams.vue'
import AppButton from './ui/AppButton.vue'
import APPModal from './ui/APPModal.vue'
import type { AddTeamProps, Team } from '@/types'
import { TeamsArray } from '@/data'

const isOpen = ref(false)
const teams = ref<Team[]>(TeamsArray)
const errorExist = ref('')

const addTeam = (teamObj: AddTeamProps) => {
  const uniqueId = crypto.randomUUID()
  const newTeamObj = { id: uniqueId, name: teamObj.name, email: teamObj.email }
  const alreadTeam = teams.value.find((team) => team.email === teamObj.email)

  if (alreadTeam) {
    errorExist.value = `This user with email ${alreadTeam.email} already exist`
    return
  }
  teams.value.push(newTeamObj)
  closeModal()
}

const openModal = () => {
  isOpen.value = true
}

const closeModal = () => {
  isOpen.value = false
  errorExist.value = ''
}

const removeTeam = (index: number) => {
  teams.value.splice(index, 1)
}

// const sortedTeams = teams.value.sort((a, b) => {
//   if (a.email < b.email) {
//     console.log('meeting')
//     return -1
//   } else {
//     return 1
//   }
// })
// console.log(sortedTeams)
</script>

<style scoped>
.app-container {
  width: 1200px;
  margin: 0 auto;
  padding: 0 48px 48px 48px;
}

.header-box {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 16px 0;
}
h1 {
  font-size: 24px;
  font-weight: 600;
}
</style>
