<script setup lang="ts">
import Student from '@/types/Student';

const props = defineProps<{
  student: Student
}>();
</script>

<template>
  <div class="p-4">
    <div 
      class="p-5 w-64 border border-gray-600 mb-4 cursor-pointer hover:scale-105 hover:shadow-lg transition-transform duration-200"
    >
      <h2 class="text-lg font-semibold">{{ student.name }} {{ student.surname }}</h2>
      <span class="text-sm text-gray-700">GPA: {{ student.gpa }}</span>
    </div>
  </div>
</template>
