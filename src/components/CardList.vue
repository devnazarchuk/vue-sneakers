<script setup>
import { inject } from 'vue';
import Card from './Card.vue'
defineProps({
  items: Array,

})
const onClickAdd = () => {
    alert("added")
}
const addToFavorite = inject('addToFavorite')
</script>
<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :title="item.title"
      :imageUrl="item.imageUrl"
      :prise="item.price"
      :onClickAdd="onClickAdd"
      :onClickFavorite="() => addToFavorite(item)"
      :isFavorite="item.isFavorite"
    />
  </div>
</template>
