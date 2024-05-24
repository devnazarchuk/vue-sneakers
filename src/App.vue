<script setup>
import { ref, provide, watch, computed } from 'vue'
import axios from 'axios'
import Drawer from './components/Drawer.vue'
import Header from './components/Header.vue'

/*Cart*(START)*/
const cart = ref([])
const isCreatingOrder = ref(false)
const isDrawerOpened = ref(false)

const totalPrice = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))
const vatPrice = computed(() => Math.round(totalPrice.value * 5) / 100)
const cartButtonDisabled = computed(() => isCreatingOrder.value || cartIsEmpty.value)
const cartIsEmpty = computed(() => cart.value.length === 0)

const closeDrawer = () => {
  isDrawerOpened.value = false
}
const openDrawer = () => {
  isDrawerOpened.value = true
}
const addToCart = (item) => {
  item.isAdded = true
  cart.value.push(item)
}
const removeFromCart = (item) => {
  item.isAdded = false
  cart.value.splice(cart.value.indexOf(item), 1)
}
const createOrder = async () => {
  try {
    isCreatingOrder.value = true
    const { data } = await axios.post('https://ea24319fe3196523.mokky.dev/orders', {
      items: cart.value,
      totalPrice: totalPrice.value
    })
    cart.value = []
    return data
  } catch (err) {
    console.log(err)
  } finally {
    isCreatingOrder.value = false
  }
}
watch(
  cart,
  () => {
    localStorage.setItem('cart', JSON.stringify(cart.value))
  },
  { deep: true }
)
provide('cart', {
  cart,
  closeDrawer,
  openDrawer,
  addToCart,
  removeFromCart
})
/*Cart*(END)*/
</script>

<template>
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" href="/logo.png" />
    <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png" />
    <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png" />
    <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png" />
    <link rel="manifest" href="/site.webmanifest" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vue Sneakers</title>
  </head>
  <Drawer
    v-if="isDrawerOpened"
    :total-price="totalPrice"
    :vat-price="vatPrice"
    @create-order="createOrder"
    :button-disabled="cartButtonDisabled"
  />
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl pt-2 w-full">
    <Header :total-price="totalPrice" @open-drawer="openDrawer" />
    <div class="p-10 h-screen overflow-y-auto" style="min-height: 90vh">
      <router-view></router-view>
    </div>
  </div>
</template>
<style>
@import url('https://fonts.googleapis.com/css2?family=Poetsen+One&family=Radio+Canada+Big:ital,wght@0,400..700;1,400..700&display=swap');
* {
  font-family: 'Poetsen One', sans-serif;
  font-weight: 500;
}
</style>
