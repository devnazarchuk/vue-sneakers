<script setup>
import { reactive, watch, ref, onMounted } from 'vue'
import axios from 'axios'
import { inject } from 'vue'
import CardList from '../components/CardList.vue'
const { cart, addToCart, removeFromCart } = inject('cart')
const items = ref([])
const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
})
const onClickAddPlus = (item) => {
  if (!item.isAdded) {
    addToCart(item)
  } else {
    removeFromCart(item)
  }
  console.log(cart)
}
const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}
const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}
const addToFavorite = async (item) => {
  try {
    if (!item.isFavorite) {
      const obj = {
        parentId: item.id,
        item
      }
      item.isFavorite = true
      const { data } = await axios.post(`https://ea24319fe3196523.mokky.dev/favorites`, obj)
      item.favoriteId = data.id
      console.log(data)
    } else {
      item.isFavorite = false
      await axios.delete(`https://ea24319fe3196523.mokky.dev/favorites/${item.favoriteId}`)
      item.favoriteId = null
    }
  } catch (err) {
    console.log(err)
  }
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(`https://ea24319fe3196523.mokky.dev/favorites`)
    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.parentId === item.id)

      if (!favorite) {
        return item
      }
      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id
      }
    })
    console.log(items.value)
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
      favoriteId: null,
      isAdded: false
    }))
  } catch (err) {
    console.log(err)
  }
}
onMounted(async () => {
  const localCart = localStorage.getItem('cart')
  if (localCart) {
    cart.value = localCart ? JSON.parse(localCart) : []
  }
  await fetchItems()
  await fetchFavorites()
  items.value = items.value.map((item) => ({
    ...item,
    isAdded: cart.value.some((cartItem) => cartItem.id === item.id)
  }))
})
watch(cart, () => {
  items.value = items.value.map((item) => ({
    ...item,
    isAdded: false
  }))
})
watch(filters, fetchItems)
</script>

<template>
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
    <CardList :items="items" @add-to-favorite="addToFavorite" @add-to-cart="onClickAddPlus" />
  </div>
</template>
