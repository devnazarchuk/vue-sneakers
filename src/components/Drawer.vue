<script setup>
import DrawerHead from './DrawerHead.vue'
import CardItemList from './CardItemList.vue'
import InfoBlock from './InfoBlock.vue'
// import { computed } from 'vue'
const emit = defineEmits(['createOrder'])
const props = defineProps({
  totalPrise: Number,
  vatPrise: Number,
  buttonDisabled: Boolean
})
</script>
<template>
  <div class="fixed top-0 left-0 w-full h-full bg-black z-10 opacity-70"></div>
  <div class="bg-white w-96 h-full fixed top-0 right-0 z-20 p-8">
    <DrawerHead />

    <div v-if="!totalPrise" class="flex h-full items-center">
    <InfoBlock
      title="Cart is empty"
      :description="'Add some sneakers to the cart'"
      imageUrl="/package-icon.png"
    />
  </div>
  <div v-else>
    <CardItemList/>

    <div class="flex flex-col gap-4 my-7">
      <div class="flex gap-2">
        <span>Subtotal:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{ totalPrise }}$</b>
      </div>

      <div class="flex gap-2">
        <span>Fee 5%:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{ vatPrise }}$</b>
      </div>
      <button
        :disabled="buttonDisabled"
        @click="() => emit('createOrder')"
        class="mt-4 bg-lime-500 w-full py-3 rounded-xl text-white disabled:bg-slate-300 hover:bg-lime-600 active:bg-lime-700 transition cursor-pointer"
      >
        <b>Checkout</b>
      </button>
    </div>
  </div>
  </div>
</template>
