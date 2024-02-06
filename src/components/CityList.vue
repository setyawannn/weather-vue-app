<template>
  <div v-for="city in savedCities" :key="city.id">
    <CityCard :city="city" @click="goToCityView(city)" />
  </div>

  <p v-if="savedCities.length === 0">
    No locations added. To start tracking a location, search in the field above.
  </p>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { LocationObj } from '../types/interface'
import axios from 'axios'
import CityCard from './CityCard.vue'
import { useRouter } from 'vue-router'

const savedCities = ref<any[]>([])

const getCities = async () => {
  const savedCitiesString = localStorage.getItem('savedCities')

  if (savedCitiesString !== null) {
    savedCities.value = JSON.parse(savedCitiesString)

    const requests: Promise<any>[] = []
    savedCities.value.forEach((city: LocationObj) => {
      requests.push(
        axios.get(
          `https://api.openweathermap.org/data/2.5/weather?lat=${city.coords.lat}&lon=${city.coords.lng}&appid=7efa332cf48aeb9d2d391a51027f1a71&units=metric`
        )
      )
    })

    const weatherData = await Promise.all(requests)

    // Delay
    await new Promise((res: any) => setTimeout(res, 1000))

    weatherData.forEach((value, index) => {
      savedCities.value[index].weather = value.data
    })
  }
}

await getCities()

const router = useRouter()
const goToCityView = (city: LocationObj) => {
  router.push({
    name: 'cityView',
    params: { state: city.state, city: city.city },
    query: {
      id: city.id,
      lat: city.coords.lat,
      lng: city.coords.lng
    }
  })
}
</script>
