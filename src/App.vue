<script>
// Sử dụng hàm ref để xác định tham chiếu phản ứng
import { ref } from "vue";
export default {
  setup() {
    const count = ref(0);
    const increase = () => count.value++;
    const decrement = () => count.value--;

    return { count, increase, decrement };
  },
};
</script>

<template>
  <h1>{{ count }}</h1>
  <button @click="increase">Tăng số</button>
  <button @click="decrement">Giảm số</button>
</template>

<style scoped>
button {
  padding: 6px 12px;
  font-size: 16px;
}
</style>
