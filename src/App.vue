<template>
	<div id="app" class="container mt-5">
		<h1>My Shop</h1>
		<p class="animated fadeInRight">Take a look at our offerings</p>
		<font-awesome-icon icon="shopping-cart"></font-awesome-icon>
		<ProductList :maximum="maximum" :products="products"></ProductList>
	</div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

import ProductList from '@/components/ProductList.vue'; // import Price from '@/components/Price.vue';

export default {
	name: "app",
	data: function () {
		return {
			maximum: 99,
			products: null
		}
	},
	components: {
		ProductList,
		FontAwesomeIcon,
	},
	mounted: function () {
		fetch('https://hplussport.com/api/products/order/price')
				.then(response => response.json())
				.then(data => {
					this.products = data;
				})
	}
};
</script>
