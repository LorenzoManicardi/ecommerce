<template>
    <div class="page-cart">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">Carrello</h1>
            </div>

            <div class="column is-12 box">
                <table class="table is-fullwidth">
                    <thead>
                        <th>Product</th>
                        <th>Price</th>
                        <th>Quantity</th>
                        <th>Total</th>
                        <th></th>
                    </thead>
                    <tbody>
                        <CartItem
                            v-for="item in carrello.items"
                            v-bind:key="item.product.id"
                            v-bind:initialItem="item" />
                    </tbody>
                </table>
            </div>

            <div class="column is-12 box">
                <h2></h2>
                <strong>${{ JSON.stringify(cartTotalPrice) }}</strong>, {{ JSON.stringify(carrello.cartTotalLength) }} items
                <hr>
                <router-link to="/cart/checkout" class="button is-dark">Go to Checkout</router-link>
            </div>

        </div>
    </div>

</template>

<script>
import axios from 'axios'
import CartItem from '@/components/CartItem.vue'

export default {
    name: 'Cart',
    components: {
        CartItem
    },

    data() {
        return {
            carrello: {
                items: []
            }
        }
    },
    mounted() {
        this.carrello = this.$store.state.cart
    },
    computed: {
        cartTotalLength() {
            let acc = 0
            return this.carrello.items.reduce((acc, curVal) => {
                return acc += currVal.quantity
            }, 0)
        },
        cartTotalPrice() {
            let acc = 0
            return this.carrello.items.reduce((acc, curVal) => {
                return acc += curVal.product.price * curVal.quantity
            }, 0)
        }
    },
}
</script>
