<template>
  <div class="flex py-6 px-3 bg-weather-secondary rounded-md shadow-md">
    <div class="flex flex-col flex-1 gap-2">
      <AnimatedPlaceholder class="max-w-[50%]" />
      <AnimatedPlaceholder class="max-w-[40%]" />
    </div>

    <div class="flex flex-col items-end flex-1 gap-2">
      <AnimatedPlaceholder class="max-w-[50%] w-full" />
      <AnimatedPlaceholder class="max-w-[70%] w-full" />
    </div>
  </div>
</template>

<script setup lang="ts">
import AnimatedPlaceholder from './AnimatedPlaceholder.vue'
</script>

<style scoped></style>
