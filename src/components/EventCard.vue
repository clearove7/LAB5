<script setup lang="ts">
import { type Event } from '@/types'
import { RouterLink } from 'vue-router'

const props = defineProps<{
  event: Event
}>()
</script>

<template>
  <RouterLink 
    :to="{ name: 'event-detail-view', params: { id: event.id } }" 
    class="text-blue-500 no-underline"
  >
    <div 
      class="cursor-pointer border border-gray-600 p-5 w-64 mb-4 hover:scale-105 hover:shadow-lg transition-transform duration-200"
    >
      <h2 class="text-lg font-semibold">{{ event.title }}</h2>
      <span class="text-sm text-gray-700">@{{ event.time }} on {{ event.date }}</span>
    </div>
  </RouterLink>
</template>
