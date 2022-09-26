<script setup lang="ts">
import { ref } from 'vue'
import ProfileItem from './ProfileItem.vue'
import Grid from 'vue-virtual-scroll-grid'
import { Profile } from '../types';
import { randomColor } from '../utils';

defineProps<{
  activeIndex?: number
}>()

const emit = defineEmits<{
  (e: 'openProfile', profile: Profile, index: number): void
}>()

const profiles = ref<Profile[]>(new Array(3000).fill(null).map((item, index) => ({ label: `Label: ${index}`, value: index.toString(), color: randomColor() })))
const scrollTo = ref<number | undefined>()

async function pageProvider(pageNumber: number, pageSize: number) {
  console.log(`pageProvider (pageNumber, pageSize) → `, pageNumber, pageSize)
  const index = pageNumber * pageSize
  return profiles.value.slice(index, index + pageSize)
}

function openProfile(profile: Profile, index: number) {
  scrollTo.value = index
  emit('openProfile', profile, index)
}
</script>

<template>
  <div class="grid-wrapper">
    <Grid class="grid" :length="profiles.length"
      :pageProvider="(pageNumber, pageSize) => pageProvider(pageNumber, pageSize)" :pageSize="100" :scrollTo="scrollTo"
      scrollBehavior="auto">
      <template v-slot:probe>
        <ProfileItem />
      </template>

      <template v-slot:placeholder="{ style }">
        <ProfileItem :style="style" />
      </template>

      <template #default="{ item, style, index }">
        <ProfileItem :profile="item" :style="style" :is-active="index === activeIndex"
          @click="openProfile(item, index)" />
      </template>
    </Grid>
  </div>
</template>

<style scoped>
.grid-wrapper {
  flex: 1;
  width: 100%;
  height: 100%;
  overflow-y: auto;
}

.grid {
  display: grid;
  place-items: start stretch;
  box-sizing: content-box;
  /* grid-template-columns: repeat(2, 1fr); */

  --column-min-width: 200px;
  --column-count-max: 7;
  --grid-item--max-width: calc(100% / var(--column-count-max));
  grid-template-columns: repeat(auto-fill, minmax(max(var(--column-min-width), var(--grid-item--max-width)), 1fr));
}
</style>
