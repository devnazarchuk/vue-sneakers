<script setup>
import Card from './Card.vue'
defineProps({
  items: Array,
  isFavorites: Boolean
})

const emit = defineEmits(['addToFavorite', 'addToCart'])
</script>
<template>
  <div class="Mesh grid grid-cols-4 gap-5 " v-auto-animate>
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :title="item.title"
      :imageUrl="item.imageUrl"
      :price="item.price"
      :onClickFavorite="isFavorites ? null : () => emit('addToFavorite', item)"
      :onClickAdd="isFavorites ? null : () => emit('addToCart', item)"
      :isFavorite="item.isFavorite"
      :isAdded="item.isAdded"
    />
  </div>
</template>
<style scoped>
  .Mesh {
    justify-content: center;
  }
@media screen and (max-width: 1440px) {
  .Mesh {
    grid-template-columns: 1fr 1fr 1fr 1fr;
  }
}
@media screen and (max-width: 1024px) {
  .Mesh {
    grid-template-columns: 1fr 1fr 1fr;
  }
}
@media screen and (max-width: 768px) {
  .Mesh {
    grid-template-columns: 1fr 1fr;
  }
  @media screen and (max-width: 425px) {
    .Mesh {
      grid-template-columns: 1fr;
    }
  }
}
</style>
