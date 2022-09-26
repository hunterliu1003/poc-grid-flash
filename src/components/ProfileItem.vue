<script setup lang="ts">
import { Profile } from '../types';

defineProps<{
  profile?: Profile
  isActive?: boolean
}>()

</script>

<template>
  <div class="profile-item" :style="{'backgroundColor': `${profile?.color}`}">
    <slot>
      {{ profile?.value }}
    </slot>
  </div>

</template>

<style scoped>
.profile-item {
  display: grid;
  justify-content: center;
  align-content: center;
  width: 100%;
  height: 100%;
  min-height: 200px;
  box-sizing: border-box;
  padding: 1rem;
  border: 1px #000 solid;
  cursor: pointer;
}
</style>