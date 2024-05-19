<script setup>
import { ref, provide, watch, computed } from 'vue'
import axios from 'axios'
import Drawer from './components/Drawer.vue'
import Header from './components/Header.vue'

/*Cart*(START)*/
const cart = ref([])
const isCreatingOrder = ref(false)
const isDrawerOpened = ref(false)

const totalPrise = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))
const vatPrise = computed(() => Math.round(totalPrise.value * 5) / 100)
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
      totalPrise: totalPrise.value
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
  <Drawer
    v-if="isDrawerOpened"
    :total-prise="totalPrise"
    :vat-prise="vatPrise"
    @create-order="createOrder"
    :button-disabled="cartButtonDisabled"
  />
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header :total-prise="totalPrise" @open-drawer="openDrawer" />
    <div class="p-10">
      <router-view></router-view>
    </div>
  </div>
</template>
