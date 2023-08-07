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


image.value = `/svg/${props.name.toLowerCase()}.svg`

</script>

<template>
  <img :src="image" :alt="alt" />
</template>

<style scoped></style>