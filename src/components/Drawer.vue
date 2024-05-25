<script setup>
import axios from 'axios'
import { ref, inject , computed } from 'vue'
import DrawerHead from './DrawerHead.vue'
import CardItemList from './CardItemList.vue'
import InfoBlock from './InfoBlock.vue'
// import { computed } from 'vue'
const props = defineProps({
  totalPrice: Number,
  vatPrice: Number,
})

const { cart, closeDrawer, openDrawer, addToCart, removeFromCart } = inject('cart')
const isCreating = ref(false)
const orderId = ref(null)
const createOrder = async () => {
  try {
    isCreating.value = true
    const { data } = await axios.post('https://ea24319fe3196523.mokky.dev/orders', {
      items: cart.value,
      totalPrice: props.totalPrice.value
    })
    cart.value = []
    orderId.value = data.id
  } catch (err) {
    console.log(err)
  } finally {
    isCreating.value = false
  }
}
const ButtonDisabled = computed(() => isCreating.value || cartIsEmpty.value)
const cartIsEmpty = computed(() => cart.value.length === 0)

</script>
<template>
  <div class="fixed top-0 left-0 w-full h-full bg-black z-10 opacity-70"></div>
  <div class="bg-white w-96 h-full fixed top-0 right-0 z-20 p-8">
    <DrawerHead />

    <div v-if="!totalPrice|| orderId" class="flex h-full items-center">
      <InfoBlock
        v-if="!totalPrice && !orderId"
        title="Cart is empty"
        description="Add some sneakers to the cart"
        imageUrl="/package-icon.png"
      />
      <InfoBlock
        v-if="orderId"
        title="Your order is confirmed"
        :description="`Your order #${ orderId } is confirmed. Thank you for shopping with us!`"
        imageUrl="/order-success-icon.png"
      />
    </div>
    <div class="scrollermenu" v-else>
      <CardItemList />

      <div class="flex flex-col gap-4 my-7">
        <div class="flex gap-2">
          <span>Subtotal:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>{{ totalPrice }}$</b>
        </div>

        <div class="flex gap-2">
          <span>Fee 5%:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>{{ vatPrice }}$</b>
        </div>
        <button
          :disabled="ButtonDisabled"
          @click="createOrder"
          class="mt-4 bg-lime-500 w-full py-3 rounded-xl text-white disabled:bg-slate-300 hover:bg-lime-600 active:bg-lime-700 transition cursor-pointer"
        >
          <b>Checkout</b>
        </button>
      </div>
    </div>
  </div>
</template>
<style scoped>
.scrollermenu {
  width: 100%;
  height: 600px;
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
