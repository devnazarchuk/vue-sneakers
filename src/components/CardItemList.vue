<script setup>
import { inject } from 'vue'
import CardItem from './CardItem.vue'

const { cart, removeFromCart } = inject('cart')
</script>
<template>
  <div class="flex flex-col flex-1 gap-4 justify-between" v-auto-animate>
    <CardItem
      v-for="item in cart"
      :key="item.id"
      :title="item.title"
      :prise="item.price"
      :imageUrl="item.imageUrl"
      @on-click-remove="() => removeFromCart(item)"
    />
  </div>
</template>
