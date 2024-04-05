<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  }
}
</script>

<template>
  <wrapper>
    <h1>Hello World</h1>
    <h1>{{ count }}</h1>
    <button @click="increment">+</button>
  </wrapper>
</template>

<style scoped></style>
