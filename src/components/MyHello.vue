<script setup>
const props = defineProps({
  title: String,
  prise: Number,
  isAdded: Boolean,
})

console.log(props)
</script>

<template>
  <div class="product">
    <h2>Product:{{ title }}</h2>
    <h3>Prise:{{ prise }}</h3>
    <h3>Added:{{ isAdded }}</h3>
    <slot></slot>
  </div>
</template>

<style scoped>
.product {
  border: 1px solid blue;
  padding: 10px;
  margin-bottom: 10px;
}
</style>
