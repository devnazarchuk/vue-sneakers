<script setup>
defineProps({
  totalPrice: Number
})

const emit = defineEmits(['openDrawer'])
</script>

<template>
  <header class="Mesh flex justify-between border-b border-slate-100 px-10 py-4 flex-wrap gap-x-[5vw]">
    <router-link to="/" class="mx-auto text-center">
      <div class="flex items-center gap-4 h-full flex-wrap justify-center">
        <img src="/public/favicon_logo/android-chrome-512x512.png" alt="Logo" class="imgLogo" />
        <div>
          <h2 class="text-xl font-bold uppercase">✨Vue Sneakers✨</h2>
          <p class="text-slate-400">Shop with the best sneakers</p>
        </div>
      </div></router-link
    >
    <ul class="flex items-center gap-[5vw] mt-3 mx-auto flex-wrap justify-center">
      <router-link to="/">
      <li class="flex items-center gap-1 cursor-pointer text-gray-500 hover:text-black">
        <img src="/shop.svg" alt="Shop" />
        <span>Shop</span>
      </li>
      </router-link>
      <li
        @click="emit('openDrawer')"
        class="flex items-center gap-1 cursor-pointer text-gray-500 hover:text-black"
      >
        <img src="/cart.svg" alt="Cart" />
        <span>{{ totalPrice }}$</span>
      </li>
      <router-link to="/favorites">
        <li class="flex items-center gap-1 cursor-pointer text-gray-500 hover:text-black">
          <img src="/heart.svg" alt="Heart" />
          <span>Favorites</span>
        </li></router-link
      >
      <router-link to="/orders">
      <li class="flex items-center gap-1 cursor-pointer text-gray-500 hover:text-black">
        <img src="/order.svg" alt="Orders" />
        <span>Orders</span>
      </li>
      </router-link>
    </ul>
  </header>
</template>
<style>
  .imgLogo{
    width: 4rem;
  }
@media screen and (max-width: 425px) {
  .imgLogo{
    width: 10rem;
  }
}
</style>
