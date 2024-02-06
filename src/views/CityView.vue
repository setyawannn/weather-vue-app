<template>
  <div>
    <Suspense>
      <AsyncCityView />
      <template #fallback>
        <CityViewSkeleton />
      </template>
    </Suspense>
  </div>
</template>

<script setup lang="ts">
import CityViewSkeleton from '@/components/CityViewSkeleton.vue'
import AsyncCityView from '../components/AsyncCityView.vue'
</script>
