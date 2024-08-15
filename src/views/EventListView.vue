<script setup lang="ts">
import { ref, onMounted, watchEffect, defineProps, computed } from 'vue'
import EventCard from '@/components/EventCard.vue'
import EventDetails from '@/components/EventDetails.vue'
import EventService from '@/services/EventService'
import { type Event } from '@/types'

const props = defineProps({
  page: {
    type: Number,
    required: true
  },
  perPage: {
    type: Number,
    required: true
  }
})

const events = ref<Event[] | null>(null)
const totalEvents = ref(0)
const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / props.perPage)
  return props.page < totalPages
})

onMounted(() => {
  watchEffect(() => {
    EventService.getEvents(props.perPage, props.page)
      .then((response) => {
        events.value = response.data
        totalEvents.value = parseInt(response.headers['x-total-count'], 10)
      })
      .catch((error) => {
        console.error('There was an error!', error)
      })
  })
})
</script>

<template>
  <div class="p-4">
    <h1 class="text-2xl font-bold mb-4">Events For Good</h1>
    <div class="flex flex-col items-center">
      <EventCard v-for="event in events" :key="event.id" :event="event" />
      <EventDetails v-for="event in events" :key="event.id" :event="event" />
      <div class="flex gap-4 mt-4">
        <RouterLink
          v-if="props.page > 1"
          :to="{ name: 'event-list-view', query: { page: props.page - 1, perPage: props.perPage }}"
          class="text-blue-500 hover:underline"
          rel="prev"
        >
          &#60; Prev page
        </RouterLink>
        <RouterLink
          v-if="hasNextPage"
          :to="{ name: 'event-list-view', query: { page: props.page + 1, perPage: props.perPage }}"
          class="text-blue-500 hover:underline"
          rel="next"
        >
          Next Page &#62;
        </RouterLink>
      </div>
    </div>
  </div>
</template>
