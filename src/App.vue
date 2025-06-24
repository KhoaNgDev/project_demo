<script>
import { ref } from "vue";
export default {
  setup() {
    const count = ref(0)
    const increase = () => count.value++

    return { count, increase }
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
