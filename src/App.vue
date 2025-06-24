<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increase() {
      this.count++
    }
  }
}
</script>

<template>
  <h1>{{ count }}</h1>
  <button @click="increase">Tăng số</button>
</template>

<style scoped>
button {
  padding: 6px 12px;
  font-size: 16px;
}
</style>
