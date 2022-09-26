<script setup lang="ts">
import { ref } from "vue";
import ProfilesGrid from "./components/ProfilesGrid.vue";
import ProfileDetail from "./components/ProfileDetail.vue";
import { Profile } from "./types";

const activeProfile = ref<Profile>()
</script>

<template>
  <div class="root">
    <ProfilesGrid @click-profile-item="(profile) => (activeProfile = profile)" />
    <ProfileDetail v-if="activeProfile" :profile="activeProfile" @close="activeProfile = undefined" />
  </div>
</template>


<style scoped>
.root {
  display: flex;
  width: 100%;
  height: 100vh;
}
</style>