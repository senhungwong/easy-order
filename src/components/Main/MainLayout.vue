<template>
    <v-flex style="height: 100%; backgroundColor: #EFEBE9;">
        <v-container style="height: 96px;"></v-container>
        <v-container>
            <items></items>
        </v-container>
        <item-modal></item-modal>
        <auth v-if="logining"></auth>
        <shopping-cart v-if="showCart"></shopping-cart>
    </v-flex>
</template>

<script>
import Items from './Items/Items';
import ItemModal from './Items/ItemModal';
import Auth from '../Share/Auth/AuthLayout';
import ShoppingCart from '../Share/ShoppingCart/ShoppingCart';

export default {
    components: {
        Items,
        ItemModal,
        Auth,
        ShoppingCart
    },
    computed: {
        logining() {
            return this.$store.getters.isLogining;
        },
        showCart() {
            return this.$store.getters.getShowCartModal;
        }
    }
}
</script>

<style>

</style>
