<!-- src/views/event/EditView.vue -->
<script setup lang="ts">
import { toRef } from 'vue'
import { type Event } from '@/types'
import { useRouter } from 'vue-router'
import { useMessageStore } from '@/stores/message'

const props = defineProps<{ passenger: Event | undefined }>()
const store = useMessageStore();
const router = useRouter();
const updatePassenger = () => {
  store.updateMessage(`Updating Passenger ${props.passenger?.name}...`)
  setTimeout(() => {
    store.resetMessage()
    router.push({name: 'passenger-detail-view'})
  }, 5000)


}
</script>

<template>
  <div class="flex justify-center mt-4 text-center">
    <div>
      <h1 class="text-xl font-bold">Edit Passenger</h1>
      <button @click="updatePassenger" class="text-white bg-blue-400 p-2 rounded">Update Passenger</button>
    </div>
  </div>
</template>

<style scoped>

</style>