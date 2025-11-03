<script setup>
import { ref, computed } from 'vue'
import socksImage from './assets/images/socks_blue.jpeg'

const product = ref('Socks')

const inventory = ref(11)

const stockStatus = computed(() => {
  if (inventory.value > 10) {
    return 'En stock'
  } else if (inventory.value >= 1 && inventory.value <= 10) {
    return 'Faible stock'
  } else {
    return 'En rupture de stock'
  }
})
</script>

<template>
  <div>
    <h1>{{ product }}</h1>
    <img :src="socksImage" alt="Socks" style="width: 120px; height: auto;" />

    <p>{{ stockStatus }}</p>
  </div>
</template>
