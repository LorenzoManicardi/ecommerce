<template>
    <div class="title">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title has-text-centered">Checkout</h1>
            </div>

            <div class="column is-12 box">
                <table class="table is-fullwidth">
                    <thead>
                        <tr>
                            <th>Product</th>
                            <th>Price</th>
                            <th>Quantity</th>
                            <th>Total</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr 
                            v-for="item in carrello.items"
                            v-bind:key="item.product.id"   
                        >
                            <td>{{ item.product.name }}</td>
                            <td>{{ item.product.price }}</td>
                            <td>{{ item.quantity }}</td>
                            <td>{{ getItemTotal(item).toFixed(2) }}</td>
                        </tr>
                    </tbody>
                    <tfoot>
                        <tr>
                            <td>Total</td>
                            <td>{{ cartTotalLength }}</td>
                        </tr>
                    </tfoot>
                </table>
            </div>

            <div class="column is-12 box">
                <h2 class="subtitle has-text-centered">Shipping Details</h2>
                <p class="has-text-grey">All fields are required</p>
                <div class="columns is-multiline">
                    <div class="column is-6">
                        <div class="field">
                            <label class="has-text-black">First Name</label>
                            <div class="control">
                                <input type="text" class="input" v-model="first_name">
                            </div>
                        </div>

                        <div class="field">
                            <label class="has-text-black">Last Name</label>
                            <div class="control">
                                <input type="text" class="input" v-model="last_name">
                            </div>
                        </div>

                        <div class="field">
                            <label class="has-text-black">E-mail</label>
                            <div class="control">
                                <input type="email" class="input" v-model="email">
                            </div>
                        </div>

                        <div class="field">
                            <label class="has-text-black">Phone</label>
                            <div class="control">
                                <input type="text" class="input" v-model="phone">
                            </div>
                        </div>
                    </div>
                    <div class="column is-6">
                        <div class="field">
                            <label class="has-text-black">Adress</label>
                            <div class="control">
                                <input type="text" class="input" v-model="adress">
                            </div>
                        </div>

                        <div class="field">
                            <label class="has-text-black">Zipcode</label>
                            <div class="control">
                                <input type="text" class="input" v-model="zipcode">
                            </div>
                        </div>

                        <div class="field">
                            <label class="has-text-black">Place</label>
                            <div class="control">
                                <input type="text" class="input" v-model="place">
                            </div>
                        </div>
                    </div>
                
                    <div class="notification is-danger mt-4">
                        <p v-for="error in errors" v-bind:key="error">{{error}}</p>
                    
                    <hr>
                    
                    <div id="card-element" class="mb-5"></div>
                    <template v-if="items">
                    
                        <hr>
                        <button class="button is-dark" @click="submitForm">Pay with Stripe</button>    
                    </template>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Checkout',
    data() {
        return {
            carrello: {
                items: []
            },
            stripe: {},
            card: {},
            first_name: '',
            last_name: '',
            email: '',
            phone: '',
            address: '',
            zipcode: '',
            place: '',
            errors: [],
        }
    },
    mounted() {
        document.title = 'Checkout - ManicardiShop'
        this.carrello = this.$store.state.cart
    },
    methods: {
        getItemTotal(item) {
            return item.quantity * item.product.price
        },
        submitForm() {
            if (this.first_name === '') {
                this.errors.push('The first name is missing!')
            }
            if (this.second_name === '') {
                this.errors.push('The first name is missing!')
            }
            if (this.email === '') {
                this.errors.push('The first name is missing!')
            }
            if (this.phone === '') {
                this.errors.push('The first name is missing!')
            }
            if (this.adress === '') {
                this.errors.push('The first name is missing!')
            }
            if (this.zipcode === '') {
                this.errors.push('The first name is missing!')
            }
            if (this.place === '') {
                this.errors.push('The first name is missing!')
            }
        }
    },
    computed: {
        cartTotalLength() {
            return this.carrello.items.reduce((acc, curVal) => {
                return acc += currVal.quantity
            }, 0)
        },
        cartTotalPrice() {
            return this.carrello.items.reduce((acc, curVal) => {
                return acc += curVal.product.price * curVal.quantity
            }, 0)
        }
    }
}
</script>