<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import CardList from '../components/CardList.vue'
const orders = ref([])
onMounted(async () => {
  try {
    const { data } = await axios.get('https://ea24319fe3196523.mokky.dev/orders')
    orders.value = data.flatMap(order => order.items)
    console.log(data)
  } catch (err) {
    console.log(err)
  }
})
</script>
<template>
    <h1 class="text-3xl font-bold mb-8">My Orders:</h1>
    <CardList :items="orders" :hide-icons="true" class="scrollermenu" />
</template>
<style scoped>
.scrollermenu {
  width: 100%;
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
