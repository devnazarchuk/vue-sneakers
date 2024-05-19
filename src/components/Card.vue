<script setup>
const props=defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  prise: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickFavorite: Function,
  onClickAdd: Function
})
const visibleFavoriteButton = Boolean(props.onClickFavorite)
</script>
<template>
  <div
    class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl"
  >
    <img src="/like-2.svg" alt="Like" class="absolute top-8 left-8" />
    <img
      v-if="visibleFavoriteButton"
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
        <b>{{ prise }}₴</b>
      </div>
      <img v-if="onClickFavorite" @click="onClickAdd" :src="isAdded ? '/checked.svg' : '/plus.svg'" alt="Plus" />
    </div>
  </div>
</template>
