<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
const favorites = ref([])
onMounted(async () => {
  try {
    const { data } = await axios.get('https://ea24319fe3196523.mokky.dev/favorites');
    favorites.value = data
    console.log(data)
  } catch (err) {
    console.log(err)
  }
})
</script>
<template>
  <h1>Favorites</h1>
</template>
