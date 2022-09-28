<script setup lang="ts">
import { onMounted } from 'vue';
import { Profile } from '../types';

const props = defineProps<{
  profile?: Profile
  isActive?: boolean
}>()

onMounted(() => {
  console.log(`ProfileItem Mounted → `, props.profile?.value)
})
</script>

<template>
  <div class="profile-item" :class="{'active': isActive }" :style="{'backgroundColor': `${profile?.color}`}">

    <slot>
      <div v-if="isActive">Active profile</div>
      <div>{{ profile?.value }}</div>
    </slot>
  </div>

</template>

<style scoped>
.profile-item {
  box-sizing: border-box;
  display: grid;
  justify-content: center;
  align-content: center;
  width: 100%;
  height: 100%;
  min-height: 200px;
  padding: 1rem;
  border: 10px solid #fff;
  text-align: center;
  font-size: 1.5rem;
  cursor: pointer;
}

.profile-item.active {
  border: 10px solid #000;
}
</style>