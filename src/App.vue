<script setup lang="ts">
import { RouterLink, RouterView, useRouter, useRoute } from 'vue-router'
import { useMessageStore } from './stores/message';
import { storeToRefs } from 'pinia';
import { ref } from 'vue'
import { SpeedInsights } from '@vercel/speed-insights/next';

const perPage = ref(2)
const router = useRouter()
const route = useRoute()
const store = useMessageStore()
const { message } = storeToRefs(store)

function updatePerPage(size: number) {
  perPage.value = size
  router.push({ name: 'event-list-view', query: { page: 1, perPage: size } })
}
</script>

<template>
  <SpeedInsights />
  <div class="text-center font-sans text-gray-700 antialias">
    <header>
      <div id="flashMessage" class="animate-fade" v-if="message">
        <h4>{{ message }}</h4>
      </div>
      <h1>Deploy with Vercel</h1>
      <div class="wrapper">
        <nav>
          <nav class="py-6">
          <RouterLink class="font-bold text-gray-700" exact-active-class="text-green-500" :to="{ name: 'event-list-view'}">Event</RouterLink> |
          <RouterLink class="font-bold text-gray-700" exact-active-class="text-green-500" :to="{ name: 'about'}">About</RouterLink> |
          <RouterLink :to="{ name: 'student' }">Student</RouterLink>
          </nav>
        </nav>
      </div>
    </header>
    <div class="pagination-controls">
      <button @click="updatePerPage(1)">Show 1 per page</button>
      <button @click="updatePerPage(2)">Show 2 per page</button>
      <button @click="updatePerPage(3)">Show 3 per page</button>
      <button @click="updatePerPage(4)">Show 4 per page</button>
      <button @click="updatePerPage(5)">Show 5 per page</button>
      <button @click="updatePerPage(6)">Show 6 per page</button>
    </div>
    <RouterView :key="$route.fullPath" />
  </div>
</template>
