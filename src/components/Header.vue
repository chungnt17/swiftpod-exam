<script setup lang="ts">
import { RouterLink } from 'vue-router'
import CartIcon from '@/components/icons/Cart.vue'

defineProps<{
    productsCount: number
}>()
</script>
<template>
    <header class="container-fluid">
        <div class="d-flex justify-content-between">
            <div class="logo">
                <b>SWIFTPOD</b>
            </div>

            <nav>
                <RouterLink to="/">HOME</RouterLink>
                <RouterLink to="/products">PRODUCT</RouterLink>
                <RouterLink to="/cart">CART</RouterLink>
            </nav>
            <div>
                <CartIcon />
                <span v-if="productsCount > 0" class="count-products">{{ productsCount }}</span>
            </div>
        </div>
    </header>
</template>
<style scoped>
.count-products {
    width: 20px;
    height: 20px;
    border: solid 1px #f00;
    border-radius: 50%;
    color: #fff;
    background-color: #de6e6e;
    padding: 0px;
    position: absolute;
    right: -10px;
    font-size: 13px;
    text-align: center;
}
</style>