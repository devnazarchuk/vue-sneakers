<script setup>
import Card from './Card.vue'

const onClickAdd = () => {
    alert("added")
}
</script>
<template>
  <div class="grid grid-cols-4 gap-4">
    <Card
      title="Air Force"
      imageUrl="/sneakers/sneakers-1.jpg"
      :prise="100"
      :isAdded="true"
      :isFavorite="true"
      :onClickAdd="onClickAdd"
    />
    <Card title="Air Jordan" imageUrl="/sneakers/sneakers-2.jpg" :prise="110" />
    <Card title="Converse" imageUrl="/sneakers/sneakers-3.jpg" :prise="120" />
    <Card title="Air Max" imageUrl="/sneakers/sneakers-4.jpg" :prise="130" />
    <Card title="Blazer" imageUrl="/sneakers/sneakers-5.jpg" :prise="140" />
  </div>
</template>
