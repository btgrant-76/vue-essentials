<template>
	<div>
		<h1>My Shop</h1>
		<navbar
				:cart="cart"
				:cartQty="cartQty"
				:cartTotal="cartTotal"
		></navbar>
		<p class="animated fadeInRight">Take a look at our offerings</p>
		<font-awesome-icon icon="shopping-cart"></font-awesome-icon>
		<PriceSlider :sliderStatus="sliderStatus" :maximum.sync="maximum"></PriceSlider>
		<ProductList
				:maximum="maximum"
				:products="products"
		></ProductList>
	</div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';
import PriceSlider from '@/components/PriceSlider.vue';
import ProductList from '@/components/ProductList.vue';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

export default {
	name: "Products",
	props: [
			'products',
			'maximum',
			'cart',
			'cartQty',
			'cartTotal',
			'sliderStatus',
			'sliderState'
	],
	components: {
		Navbar,
		ProductList,
		PriceSlider,
		FontAwesomeIcon
	}
}
</script>

<style scoped>

</style>
