<script setup lang="ts">
import { reactive } from 'vue'
import { RouterView } from 'vue-router'
import Header from '@/components/Header.vue'


const computedProductsCount = () => {
    const products = JSON.parse(localStorage.getItem('products') || '[]');
    return products.length;
}
const cart = reactive({
    productsCount: computedProductsCount()
})
const updateProductsCount = (value: number) => {
    cart.productsCount += value;
}

</script>

<template>
    <Header :productsCount="cart.productsCount" />
    <main class="container">
        <RouterView @on-change-products-count="updateProductsCount" />
    </main>
</template>

<style>
@import '@/assets/base.css';

nav a {
    color: black;
    text-transform: uppercase;
    margin: 0px 15px;
}

nav a.router-link-active {
    color: blue;
}
</style>
