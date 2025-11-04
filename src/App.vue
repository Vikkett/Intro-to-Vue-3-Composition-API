<script setup>
import { ref, computed } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'

const brand = ref("CPNV")
const product = ref("Socks")
const details = ref(['50% cotton', '30% wool', '20% polyester'])
const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage, quantity: 10 },
  { id: 2235, color: 'blue',  image: socksBlueImage,  quantity: 0 }
])

const selectedVariant = ref(0)
const cart = ref(0)
const title = computed(() => brand.value + " " + product.value)
const image = computed(() => {
  return variants.value[selectedVariant.value].image
})

const inStock = computed(() => {
  return variants.value[selectedVariant.value].quantity > 0
})

const addToCart = () => {
  if (inStock.value) cart.value++
}

const updateVariant = (index) => {
  selectedVariant.value = index
  console.log("selectedVariant = ", selectedVariant.value)
}
</script>


<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
  
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image" />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-for="detail in details" :key="detail">
            {{ detail }}
          </li>
        </ul>
        <div 
          v-for="(variant, index) in variants"
          :key="variant.id"
          @mouseover="updateVariant(index)"
        >
          {{ variant.color }}
        </div>
        <button 
          class="button" 
          @click="addToCart"
          :disabled="!inStock"
        >
          Add to cart
        </button>

      </div>
    </div>
  </div>
</template>
