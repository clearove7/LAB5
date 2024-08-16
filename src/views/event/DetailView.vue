<!-- src/views/event/DetailView.vue -->
<script setup lang="ts">
import { toRefs, defineProps, onMounted } from 'vue'
import { type Event } from '@/types'
import { useMessageStore } from '@/stores/message'
import { storeToRefs } from 'pinia'
 
const props = defineProps<{
  event: Event
  id: String
}>()
const { event } = toRefs(props)
const store = useMessageStore()
const { message } = storeToRefs(store)
 
onMounted(() => {
  if (message.value) {
    setTimeout(() => {
      store.resetMessage()
    }, 3000)
  }
})
</script>
 
<template>
  <div v-if="message" id="flashMessage">
    <h4>{{ message }}</h4>
  </div>
  <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
  <p>{{ event.description }}</p>
</template>
 
<style scoped>
@keyframes yellofade {
  from {
    background-color: yellow;
  }
  to {
    background-color: transparent;
  }
}
#flashMessage {
  animation: yellofade 3s ease-in-out;
}
</style>
 