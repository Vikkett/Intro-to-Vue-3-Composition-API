<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'

const product = ref('Chaussettes')
const image = ref(socksGreenImage)
const inStock = ref(true)
const cart = ref(0)
const details = ref(['50% coton', '30% laine', '20% polyester'])
const variants = ref([{id: 2234, color: 'green', image: socksGreenImage},
                      {id: 2235, color: 'blue', image: socksBlueImage}])

function addToCart() {
  cart.value++
}
function removeFromCart() {
  if (cart.value > 0) {
    cart.value--
  }
}
function changeImage(itemPath) {
  image.value = itemPath
}
</script>

<template>
  <div class="nav-bar">
    Panier : {{ cart }}
  </div>

  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image" alt="Image du produit">
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inStock">En stock</p>
        <p v-else>Rupture de stock</p>

        <ul>
          <li v-for="detail in details" :key="detail">{{ detail }}</li>
        </ul>
        <div class="color-variants">
          <p>Couleurs disponibles :</p>
          <div
            v-for="variant in variants"
            :key="variant.id"
            class="color-circle"
            :style="{ backgroundColor: variant.color }"
            @mouseover="changeImage(variant.image)"
          ></div>
        </div>
        <button @click="addToCart">Ajouter au panier</button>
        <button @click="removeFromCart">Enlever du panier</button>
      </div>

    </div>
  </div>
</template>



<style>
.nav-bar {
  background-color: #42b983;
  color: white;
  padding: 10px;
  font-weight: bold;
  font-size: 18px;
}

.product-display {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

.product-container {
  display: flex;
  align-items: flex-start;
  gap: 30px;
}

.product-image img {
  width: 250px;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}

.product-info {
  max-width: 300px;
}

.color-variants {
  margin: 10px 0;
}

.color-circle {
  width: 25px;
  height: 25px;
  border-radius: 50%;
  display: inline-block;
  margin-right: 8px;
  cursor: pointer;
  border: 1px solid #ccc;
}

button {
  margin: 5px;
  padding: 8px 12px;
  cursor: pointer;
  background-color: #462c9d;
  border: none;
  color: white;
  border-radius: 5px;
  font-weight: 600;
  transition: 0.3s;
}

button:hover {
  background-color: #462c9d;
}
</style>
