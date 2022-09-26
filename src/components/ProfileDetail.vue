<script setup lang="ts">
import { Profile } from '../types';

const props = defineProps<{
  profile?: Profile
  isActive?: boolean
}>()

const emit = defineEmits<{
  (e: 'close'): void
}>()
</script>

<template>
  <div class="profile" :style="{'backgroundColor': `${profile?.color}`}">
    <button @click="emit('close')">close profile</button>
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