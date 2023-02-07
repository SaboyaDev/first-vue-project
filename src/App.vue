<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'
const product = ref('Socks')
const image = ref(socksGreenImage)
// const image2 = ref(socksBlueImage)
const inStock = ref(true)
const details = ref(['50% cotton', '30% wool', '20% polyster'])
const variants = ref([
	{ id: 2234, color: 'Green', image: socksGreenImage },
	{ id: 2235, color: 'Blue', image: socksBlueImage },
])
const cart = ref(0)
const addToCart = () => ++cart.value
const updateImage = variantImage => {
	image.value = variantImage
}
</script>

<template>
	<div class="nav-bar"></div>
	<div class="cart">Cart({{ cart }})</div>
	<div class="product-display">
		<div class="product-container">
			<div class="product-image">
				<!-- Image Goes Here -->
				<img v-bind:src="image" />
			</div>
			<div class="product-info">
				<h1>{{ product }}</h1>
				<p v-if="inStock">In Stock</p>
				<p v-else>Out of Stock</p>
				<ul>
					<li v-for="detail in details">{{ detail }}</li>
				</ul>
				<div class="variants">
					<button
						class="variant button"
						v-for="variant in variants"
						:key="variant.id"
						:style="[{ 'background-color': variant.color }]"
						@click="updateImage(variant.image)"
					>
						<!-- {{ variant.color }} -->
					</button>
				</div>
				<button
					class="add-to-cart button"
					@click="addToCart"
				>
					Add to Cart
				</button>
			</div>
		</div>
	</div>
</template>
