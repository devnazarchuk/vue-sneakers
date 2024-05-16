<script setup>
import { onMounted, reactive, ref, watch } from 'vue'
import axios from 'axios'
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
// import Drawer from './components/Drawer.vue'

const items = ref([])

const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
})
const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}
const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}
const fetchFavorites = async () => {
  try {
    const { data } = await axios.get(`https://ea24319fe3196523.mokky.dev/favorites`)
    items.value = data.value.map(item => {
      const favorite = favorite.find(favorite => favorite.parentId === item.id);

      if (!favorite) {
         return item
      }
      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id,
      }
     


    })
  } catch (err) {
    console.log(err)
  }
}
const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get(`https://ea24319fe3196523.mokky.dev/items`, { params })
    items.value = data.map((obj) => ({
        ...obj,
        isFavorite: false,
        isAdded: false
    }))
  } catch (err) {
    console.log(err)
  }
}
onMounted(async() => {
  await fetchItems();
  await fetchFavorites();
})
watch(filters, fetchItems)
</script>

<template>
  <!-- <Drawer /> -->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header />
    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Sneakers for every occassion</h2>

        <div class="flex gap-4">
          <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
            <option value="name">Filter by name</option>
            <option value="price">Filter by price(cheap)</option>
            <option value="-price">Filter by price(exspensive)</option>
          </select>

          <div class="relative">
            <img class="absolute left-4 top-3" src="/search.svg" />
            <input
              @input="onChangeSearchInput"
              type="text"
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
              placeholder="Search"
            />
          </div>
        </div>
      </div>
      <div class="mt-10">
        <CardList :items="items" />
      </div>
    </div>
  </div>
</template>
