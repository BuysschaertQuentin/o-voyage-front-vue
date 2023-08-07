<script setup lang="ts">
import { ref, computed } from 'vue'
import countries from '@/datas/countries.json'

const props = defineProps({
  name: {
    type: String,
    required: true
  }
})

const alt = computed(() => `Drapeau de ${props.name}`)
const image = ref()
const url = `https://o-voyage-en-vue-9gnia.ondigitalocean.app/svg`
const country = countries.find((country) => country.name === props.name)

if(country)
image.value = `${url}/${country.code.toLowerCase()}.svg`

</script>

<template>
  <img :src="image" :alt="alt" />
</template>

<style scoped></style>