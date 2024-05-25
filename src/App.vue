<script setup>
import { ref, provide, watch, computed } from 'vue'
// import axios from 'axios'
import Drawer from './components/Drawer.vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue';
/*Cart*(START)*/
const cart = ref([])

const isDrawerOpened = ref(false)

const totalPrice = computed(() => 
  cart.value.filter(item => item !== null && item !== undefined)
            .reduce((acc, item) => acc + item.price, 0)
);
const vatPrice = computed(() => Math.round(totalPrice.value * 5) / 100)

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
    <link rel="icon" href="/public/favicon_logo/logo.png" />
    <link rel="apple-touch-icon" sizes="180x180" href="/public/favicon_logo/apple-touch-icon.png" />
    <link rel="icon" type="image/png" sizes="32x32" href="/public/favicon_logo/favicon-32x32.png" />
    <link rel="icon" type="image/png" sizes="16x16" href="/public/favicon_logo/favicon-16x16.png" />
    <link rel="manifest" href="/public/favicon_logo/site.webmanifest" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vue Sneakers</title>
  </head>
  <Drawer
    v-if="isDrawerOpened"
    :total-price="totalPrice"
    :vat-price="vatPrice"
  />
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl pt-2 w-full">
    <Header :total-price="totalPrice" @open-drawer="openDrawer" />
    <div class="p-10 h-full overflow-y-auto" style="min-height: 90vh">
      <router-view></router-view>
    </div>
    <Footer/>
  </div>
</template>
<style>
@import url('https://fonts.googleapis.com/css2?family=Poetsen+One&family=Radio+Canada+Big:ital,wght@0,400..700;1,400..700&display=swap');
* {
  font-family: 'Poetsen One', sans-serif;
  font-weight: 500;
}
</style>
