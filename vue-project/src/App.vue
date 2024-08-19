<script setup lang="ts">
import { onMounted, ref } from 'vue'

const health = ref<string[]>([])

onMounted(() => {
  setInterval(async () => {
    const response = await fetch('http://localhost:8080/actuator/metrics/process.cpu.usage')
    const data = await response.json()
    health.value.push(data.measurements[0].value)
  }, 500)
})
</script>

<template>
  <p>{{ health }}</p>
</template>
