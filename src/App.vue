<script setup>
import Header from './components/Header.vue'
</script>

<template>
  <div class="bg-white w-4/5 m-auto h-screen rounded-xl shadow-xl mt-14">
    <Header />

    <div class="">
      <div class="relative m-10 border border-slate-100 rounded-3xl">
        <img src="/like-2.svg" alt="Like" class="absolute top-0 left-0"/>
      </div>
      <img src="/public/sneakers/sneakers-1.jpg" alt="Sneaker" />
      <p>Men's Sneakers Nike Blazer Suede</p>

      <div class="flex justify-between">
        <div class="flex flex-col">
          <span class="text-slate-400">Prise:</span>
          <span>100$</span>
        </div>
        <img src="/public/plus.svg" alt="Plus" class="absolute top-0 left-0">
      </div>
    </div>
  </div>
</template>
