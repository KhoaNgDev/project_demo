<script>
import { ref, reactive } from 'vue'

export default {
  setup () {

    const message = ref("Hello")
    
    const quantity = ref(1)

    const item = reactive({
      name: "Product 1",
      price: 10
    })

    const increment = () => quantity.value++
    
    const decrement = () => quantity.value--

    const swapProduct = () => {
      item.name = "Product A"
      item.price = 30
    }

    return {
      message,
      quantity,
      increment,
      decrement,
      item,
      swapProduct
    }
  }
}
</script>

<template>
  <h1>{{ item.name }} : {{ item.price }}</h1>
  <button @click="swapProduct">Swap product</button>
  
  <h2>{{ quantity }}</h2>
  <button @click="increment">+</button>
  <button @click="decrement">-</button>
</template>

<style scoped>
</style>
