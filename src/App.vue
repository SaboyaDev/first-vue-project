<script setup>
import { ref } from 'vue'
import ProductDisplay from '@/components/ProductDisplay.vue'

const cart = ref([])
const premium = ref(false)

const updateCart = productId => cart.value.push(productId)
</script>

<template>
	<div class="nav-bar"></div>
	<div class="cart">Cart({{ cart.length }})</div>
	<ProductDisplay
		:premium="premium"
		@add-to-cart="updateCart"
	/>
</template>
