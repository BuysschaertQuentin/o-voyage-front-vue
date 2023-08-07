<script setup lang="ts">
import { ref, computed } from 'vue'

const props = defineProps({
  name: {
    type: String,
    required: true
  }
})

const alt = computed(() => `Drapeau de ${props.name}`)
const image = ref()
const url = `https://o-voyage-en-vue-9gnia.ondigitalocean.app/svg`

image.value = `${url}/${props.name.toLowerCase()}.svg`

</script>

<template>
  <img :src="image" :alt="alt" />
</template>

<style scoped></style>