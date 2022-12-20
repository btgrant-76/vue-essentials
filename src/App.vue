<template>
  <div id="app" class="container mt-5">
    <h1>My Shop</h1>
		<navbar
				:cart="cart"
				:cartQty="cartQty"
				:cartTotal="cartTotal"
				@toggle="toggleSliderStatus"
				@delete="deleteItem"
		></navbar>
    <p class="animated fadeInRight">Take a look at our offerings</p>
    <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
		<PriceSlider :sliderStatus="sliderStatus" :maximum.sync="maximum"></PriceSlider>
		<ProductList
      :maximum="maximum"
      :products="products"
      @add="addItem"
    ></ProductList>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import ProductList from "@/components/ProductList.vue"; // import Price from '@/components/Price.vue';
import PriceSlider from "./components/PriceSlider.vue";
import Navbar from '@/components/Navbar.vue';

export default {
  name: "app",
	components: {
		Navbar,
		ProductList,
		FontAwesomeIcon,
		PriceSlider
	},
	data: function() {
    return {
      maximum: 99,
      sliderStatus: true,
      cart: [],
      products: null
    };
  },
	computed: {
		cartTotal: function() {
			let sum = 0;
			for (let key in this.cart) {
				sum = sum+(this.cart[key].product.price * this.cart[key].qty);
			}
			return sum;
		},
		cartQty: function() {
			let qty = 0;
			for (let key in this.cart) {
				qty = qty + this.cart[key].qty;
			}
			return qty;
		}
	},
  methods: {
    addItem: function(product) {
      console.log(product);
      let whichProduct;
      const existing = this.cart.filter(function(item, index) {
        if (item.product.id == Number(product.id)) {
          whichProduct = index;
          return true;
        } else {
          return false;
        }
      });

      if (existing.length) {
        this.cart[whichProduct].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    },
		deleteItem: function(id) {
			if(this.cart[id].qty>1) {
				this.cart[id].qty--;
			} else {
				this.cart.splice(id, 1);
			}
		},

    /*deleteItem: function(id) {
      if (this.cart[id].qty > 1) {
        this.cart[id].qty--;
      } else {
        this.cart.splice(id, 1);
      }
    },*/
		toggleSliderStatus: function () {
			this.sliderStatus = !this.sliderStatus;
		}
  },
  mounted: function() {
    fetch("https://hplussport.com/api/products/order/price")
      .then(response => response.json())
      .then(data => {
        this.products = data;
      });
  }
};
</script>
