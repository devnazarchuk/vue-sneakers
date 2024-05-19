<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import CardList from '../components/CardList.vue'
const favorites = ref([])
const ServerUrl = 'https://ea24319fe3196523.mokky.dev'
onMounted(async () => {
  try {
    const { data } = await axios.get(
        `${ServerUrl}/favorites`
    )
    favorites.value = data.map((obj) => obj.item);
    console.log(data)
  } catch (err) {
    console.log(err)
  }
})
</script>
<template>
  <h1>Favorites</h1>
  <CardList :items="favorites" is-favorites />
</template>
