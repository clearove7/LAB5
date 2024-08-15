<script setup lang="ts">
import { type Event } from '@/types';

const props = defineProps<{
  event: Event
}>();
</script>

<template>
  <div 
    class="p-5 w-64 border border-gray-600 mb-4 flex flex-col items-end cursor-pointer hover:scale-105 hover:shadow-lg transition-transform duration-200"
  >
    <h2 class="text-lg font-semibold">{{ event.category }}</h2>
    <span class="text-sm text-gray-700">{{ event.organizer }}</span>
  </div>
</template>
