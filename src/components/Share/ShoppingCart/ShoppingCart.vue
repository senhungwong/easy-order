<template>
    <v-dialog max-width="600px" v-model="showCart">
        <v-card flat>
            <v-card-title primary-title>
                Shopping Cart
            </v-card-title>
            <v-container>
                <v-layout row wrap>
                    <v-flex xs12 v-for="item in cartItems" :key="item.id">
                        <cart-item :item="item"></cart-item>
                    </v-flex>
                </v-layout>
                <v-flex>
                    Total Price: ${{ totalPrice }}
                </v-flex>
                <v-btn flat small block :disabled="totalPrice <= 0" @click="placeOrder()">Place Order</v-btn>
            </v-container>
        </v-card>
    </v-dialog>
</template>

<script>
import { create } from '../../../VueResource/order';
import CartItem from './CartItem';

export default {
    computed: {
        showCart: {
            get: function() {
                return this.$store.getters.getShowCartModal;
            },
            set: function() {
                this.$store.commit('toggleCartShow');
            }
        },
        cartItems() {
            return this.$store.getters.getCartItems;
        },
        totalPrice() {
            return this.$store.getters.getTotalPrice;
        }
    },
    methods: {
        placeOrder() {
            let order = [];
            this.cartItems.forEach(item => {
                order.push({
                    "item_id": item.id,
                    "quantity": item.quantity
                })
            });
            create(order, this.$store.getters.getAccessToken).then(response => {
                this.$store.commit('pushToOrders', response.data.data);
                this.$store.commit('toggleCartShow');
            }, error => {
                console.log(error); //TODO: Error Message
            });
        }
    },
    components: {
        CartItem
    }
}
</script>

<style>

</style>
