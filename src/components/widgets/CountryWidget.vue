<script setup lang="ts">
import { ref, computed, watchEffect } from 'vue'
import countries from '@/datas/countries.json'
const props = defineProps({
  name: {
    type: String,
    required: true
  }
})

const alt = computed(() => `Drapeau de ${props.name}`)
const image = ref()

watchEffect(async () => {
  const country = countries.find((country) => country.name === props.name)
  if (country) {
    const { default: src } = await import(
      /*@vite-ignore*/ `${import.meta.env.VITE_BASE_URL}/svg/${country.code.toLowerCase()}.svg`
    )
    image.value = src
  }
})
</script>
<template>
  <img :src="image" :alt="alt" />
</template>
<style scoped></style>
