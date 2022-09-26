<script setup lang="ts">
import { Profile } from '../types';

defineProps<{
  profile?: Profile
}>()

const emit = defineEmits<{
  (e: 'closeProfile'): void
}>()
</script>

<template>
  <div class="profile" :style="{'backgroundColor': `${profile?.color}`}">
    <button @click="emit('closeProfile')">Close Profile</button>
    <slot>
      <pre>Profile: {{ profile }}</pre>
    </slot>
  </div>

</template>

<style scoped>
.profile {
  flex: 1;
  width: 100%;
  height: 100vh;
  box-sizing: border-box;
  padding: 1rem;
  border: 1px #000 solid;
}
</style>