<script setup>
const emit = defineEmits(['onClickRemove'])
defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  prise: Number
})
</script>
<template>
  <div class="flex items-center border border-slate-200 rounded-xl p-4 gap-4">
    <img class="w-16 h-16" :src="imageUrl" :alt="title" />
    <div class="flex flex-col flex-1">
      <p>{{ title }}</p>
      <div class="flex justify-between mt-2">
        <b class="flex-1">{{ prise }} $</b>
        <img @click="emit('onClickRemove')" class="opacity-40 hover:opacity-100 cursor-pointer transition" src="/close.svg" />
      </div>
    </div>
  </div>
</template>
