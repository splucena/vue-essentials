<template>
  <div id="app" class="container mt-5">
    <router-view :cart="cart" 
              :cartQty="cartQty" 
              :cartTotal="cartTotal" 
              @delete="deleteItem" 
              @add="addItem" 
              @toggle="toggleSliderStatus" 
              :sliderStatus="sliderStatus" 
              :maximum.sync="maximum" 
              :products="products">
    </router-view>
  </div>
</template>

<script>
import axios from 'axios';


export default {
  name: 'App',
  data: function() {
    return {
      maximum: 99,      
      sliderStatus: true,
	    products: null,
      cart: []
    }
  },
  computed: {    
    cartQty: function () {
        let qty = 0;
        for (let key in this.cart) {
            qty = qty + this.cart[key].qty;
        }

        return qty;
    },
    cartTotal: function () {
        let sum = 0;
        for (let key in this.cart) {
            sum = sum + (this.cart[key].product.price * this.cart[key].qty);
        }

        return sum;
    }
  },
  methods: {
    toggleSliderStatus: function() {
      this.sliderStatus = !this.sliderStatus;
    },
    addItem: function (product) {
      let whichProduct;
      let existing = this.cart.filter(function (item, index) {
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
        this.cart.push({
          product: product,
          qty: 1
        })
      }
    },
    deleteItem: function (id) {
        if (this.cart[id].qty > 1) {
            this.cart[id].qty--;
        } else {
            this.cart.splice(id, 1);
        }
    },            
  },
  mounted: function () {
    let url = 'https://hplussport.com/api/products/order/price';
    // axios
    axios.get(url)
      .then((data) => {
        console.log(data);
        this.products = data.data;
    })
  }
}
</script>

<style scoped>
  [v-cloak] {
              visibility: hidden;
  }

  /* https://vuejs.org/v2/guide/transitions.html */
  /* or use premade css library
    https://daneden.github.io/animate.css */
  .fade-enter,
  .fade-leave-to {
      opacity: 0;
  }

  .fade-enter-active,
  .fade-leave-active {
      transition: all 1s ease-in-out;
  }
</style>