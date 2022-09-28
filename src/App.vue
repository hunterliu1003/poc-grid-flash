<script setup lang="ts">
import { ref } from 'vue'
import ProfilesGrid from './components/ProfilesGrid.vue'
import ProfileDetail from './components/ProfileDetail.vue'
import type { Profile } from './types'

const activeProfile = ref<Profile>()
const activeIndex = ref<number>()

function openProfile(profile: Profile, index: number) {
  activeProfile.value = profile
  activeIndex.value = index
}
function closeProfile() {
  activeProfile.value = undefined
  activeIndex.value = undefined
}
</script>

<template>
  <div class="root">
    <ProfilesGrid :active-index="activeIndex" @open-profile="(profile, index) => openProfile(profile, index)" />
    <ProfileDetail v-if="activeProfile" :profile="activeProfile" @close-profile="closeProfile" />
  </div>
</template>

<style scoped>
.root {
  display: flex;
  width: 100%;
  height: 100vh;
}
</style>
