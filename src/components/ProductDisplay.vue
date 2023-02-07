<script setup>
import { ref, computed } from 'vue'
import socksGreenImage from '@/assets/images/socks_green.jpeg'
import socksBlueImage from '@/assets/images/socks_blue.jpeg'

const props = defineProps({
	premium: {
		type: Boolean,
		required: true,
	},
})

const emit = defineEmits('add-to-cart')

const product = ref('Socks')
const brand = ref('Vue Mastery')
const selectedVariant = ref(0)
const details = ref(['50% cotton', '30% wool', '20% polyster'])
const variants = ref([
	{ id: 2234, color: 'Green', image: socksGreenImage, quantity: 10 },
	{ id: 2235, color: 'Blue', image: socksBlueImage, quantity: 0 },
])

const title = computed(() => {
	return brand.value + ' ' + product.value
})

const image = computed(() => {
	return variants.value[selectedVariant.value].image
})

const inStock = computed(() => {
	return variants.value[selectedVariant.value].quantity > 0
})

const shipping = computed(() => {
	return props.premium ? 'Free' : '$2.99'
})

const productId = variants.value[selectedVariant.value].id

const addToCart = () => emit('add-to-cart', productId)

const updateSelectedVariant = index => {
	selectedVariant.value = index
}
</script>

<template>
	<div class="product-display">
		<div class="product-container">
			<div class="product-image">
				<!-- Image Goes Here -->
				<img v-bind:src="image" />
			</div>
			<div class="product-info">
				<h1>{{ title }}</h1>
				<p v-if="inStock">In Stock</p>
				<p v-else>Out of Stock</p>
				<p>Shipping: {{ shipping }}</p>
				<ul>
					<li v-for="detail in details">{{ detail }}</li>
				</ul>
				<div class="variants">
					<button
						class="variant color-circle"
						v-for="(variant, index) in variants"
						:key="variant.id"
						:style="{ backgroundColor: variant.color }"
						@click="updateSelectedVariant(index)"
					></button>
				</div>
				<button
					class="add-to-cart button"
					:class="{ disabledButton: !inStock }"
					:disabled="!inStock"
					@click="addToCart"
				>
					Add to Cart
				</button>
			</div>
		</div>
	</div>
</template>
