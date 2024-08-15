<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import EventDetails from '@/components/EventDetails.vue'
import Student from '@/types/Student'
import StudentCard from '@/components/StudentCard.vue'
import { ref, onMounted } from 'vue'
import StudentService from '@/services/StudentService'

const students = ref<Student[]>([])

onMounted(() => {
  StudentService.getEvents()
    .then((response) => {
      students.value = response.data
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
})
</script>

<template>
  <div class="p-4">
    <h1 class="text-2xl font-bold mb-6">Students List</h1>
    <div class="flex flex-col items-center">
      <StudentCard v-for="student in students" :key="student.id" :student="student" />
    </div>
  </div>
</template>
