<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import CardList from '../components/CardList.vue'
const favorites = ref([])
onMounted(async () => {
  try {
    const { data } = await axios.get(
        'https://ea24319fe3196523.mokky.dev/favorites'
    )
    favorites.value = data.map((obj) => obj.item);
    console.log(data)
  } catch (err) {
    console.log(err)
  }
})
</script>
<template>
  <h1 class="text-3xl font-bold mb-8">My favorites:</h1>
  <CardList :items="favorites" is-favorites class="scrollermenu"/>
</template>
<style scoped>
.scrollermenu {
  width: 100%;
  height: 100dvh;
  overflow-y: scroll; 
}
.scrollermenu::-webkit-scrollbar {
    width: 0;
}

.scrollermenu {
    -ms-overflow-style: none;
}

.scrollermenu {
    overflow: -moz-scrollbars-none;
}
</style>