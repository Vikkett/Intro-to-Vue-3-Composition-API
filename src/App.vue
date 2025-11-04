<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const inStock = ref(false)
  
const details = ref(['50% cotton', '30% wool', '20% polyester'])

const variants = ref([
  { id: 2234, color: 'green' },
  { id: 2235, color: 'blue' },
])

const cart = ref(0)

const addToCart = () => {
  if (inStock.value) cart.value += 1
}
</script>

<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
  
  <div class="product-display">
    <div class="product-container">
      
      <div class="product-image">    
        <img v-bind:src="image">
      </div>
      
      <div class="product-info">
        <h1>{{ product }}</h1>
        
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        
        <ul>
          <li v-for="detail in details" :key="detail">{{ detail }}</li>
        </ul>
        
        <div class="colors">
          <div
            v-for="variant in variants"
            :key="variant.id"
            :style="{ backgroundColor: variant.color }"
            class="color-circle"
          ></div>
        </div>
        
        <button
          :class="['button', !inStock ? 'disabledButton' : '']"
          :disabled="!inStock"
          @click="addToCart"
        >
          Add to Cart
        </button>
      </div>
      
    </div>
  </div>
</template>

