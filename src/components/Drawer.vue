<script setup>
import DrawerHead from './DrawerHead.vue'
import CardItem from './CardItem.vue'

</script>
<template>
  <div class="fixed top-0 left-0 w-full h-full bg-black z-10 opacity-70"></div>
  <div class="bg-white w-96 h-full fixed top-0 right-0 z-20 p-8">
    <DrawerHead />
    <CardItem />
  </div>
</template>
