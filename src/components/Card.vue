<script setup>
defineProps({
  imageUrl: String,
  title: String,
  prise: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
  onClickFavorite: Function
})
</script>
<template>
  <div
    class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl"
  >
    <img src="/like-2.svg" alt="Like" class="absolute top-8 left-8" />
    <img
      :src="isFavorite ? '/like-2.svg' : '/like-1.svg'"
      alt="Plus"
      class="absolute top-8 left-8"
      @click="onClickFavorite"
    />
    <img :src="imageUrl" />
    <p class="m-2">{{ title }}</p>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Prise:</span>
        <b>{{ prise }}$</b>
      </div>
      <img @click="onClickAdd" :src="isAdded ? '/checked.svg' : '/plus.svg'" alt="Plus" />
    </div>
  </div>
</template>
