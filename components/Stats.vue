<template>
  <div class="grid grid-cols-2 rounded-lg overflow-hidden shadow bg-gray-200 gap-px md:grid-cols-4 ">
    <div v-for="item in stats" :key="item.name" class="px-4 py-5 sm:p-6 bg-white">
      <div class="flex justify-between">
        <div class="text-base font-normal text-gray-900">
          {{ item.name }}
        </div>
        <div class="text-sm" :class="item.class">
          {{ displayPercent(item.percent) }}
        </div>
      </div>
      <div class="mt-1 flex justify-between items-baseline md:block lg:flex">
        <div class="flex items-baseline text-2xl" :class="item.class">
          {{ displayDistanceInKm(item.distance, precision) }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Collections } from '@nuxt/content';
const { getStats, displayDistanceInKm, displayPercent } = useStats();

const { voies, precision } = defineProps<{
  voies: Collections['voiesCyclablesGeojson'][];
  precision?: number;
}>();

const stats = getStats(voies);
</script>
