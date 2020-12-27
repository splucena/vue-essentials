<template>
    <nav class="navbar navbar-light fixed-top">
            <div class="navbar-text ml-auto d-flex">
                <button class="btn btn-sm btn-outline-success" @click="$parent.$emit('toggle')"><font-awesome-icon icon="dollar-sign"></font-awesome-icon></button>
                        
                <div class="dropdown ml-2" v-if="cart.length>0">
                    <!-- v-if="cart.length>0"-->
                    <button class="btn btn-success btn-sm dropdown-toggle" id="cartDropdown" data-toggle="dropdown"
                        aria-haspopup="true" aria-expanded="false">
                        <!--<b :style="{'color': badgeColor,}">cart</b>-->
                        <span class="badge badge-pill badge-light">{{ cartQty }}</span>
                        <font-awesome-icon icon="shopping-cart" class="mx-2"></font-awesome-icon>
                        {{ cartTotal | currency(cartTotal) }}
                    </button>
                    <div class="dropdown-menu dropdown-menu-right" aria-labelledby="cartDropdown">
                        <div v-for="(item, index) in cart" :key="index">
                            <div class="dropdown-item-text text-nowrap text-right">
                                <span class="badge badge-pill badge-warning align-text-top mr-1">{{ item.qty }}</span>
                                {{ item.product.name }}
                                <b class="mx-2">{{ item.product.price | currency(item.product.price) }}</b>
                                <a href="#" @click.stop="$parent.$emit('delete', index)" class="badge badge-danger text-white">-</a>                                
                            </div>
                        </div>
                        <router-link class="btn btn-sm btn-outline-info text-dark float-right mr-4 mt-2" to="/checkout">Checkout</router-link>
                    </div>
                </div>
            </div>
        </nav>
</template>

<script>
import Price from "./Price.vue";
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

export default {
    name: "navbar",  
    filters: {
        currency: function (value) {
            return '$' + Number.parseFloat(value).toFixed(2);
        }
    },
    props: ["cart", "cartQty", "cartTotal"],
    components:  {
        FontAwesomeIcon,
        Price
    }   
}
</script>