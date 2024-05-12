<script setup>
defineProps({
  imageUrl : String,
  title : String
})
</script>
<template>
      <div class="relative m-10 bg-yellow border border-slate-100 rounded-3xl cursor-pointer hover:translate-y-[-2px] hover:shadow-xl">
        <img src="/like-2.svg" alt="Like" class="absolute top-1 left-1" />
        <img :src="imageUrl" alt="Sneaker" />
        <p class="m-2">{{ title }}</p>

        <div class="flex justify-between m-2">
          <div class="flex flex-col">
            <span class="text-slate-400">Prise:</span>
            <b>100$</b>
          </div>
          <img src="/plus.svg" alt="Plus"/>
        </div>
      </div>
</template>