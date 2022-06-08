<script setup lang="ts">
import ProductItem from '@/components/ProductItem.vue';
const emit = defineEmits('on-change-products-count');
const products = [
    {
        id: 1,
        image: 'https://via.placeholder.com/160x90.png',
        name: 'example 1',
        price: 10
    },
    {
        id: 2,
        image: 'https://via.placeholder.com/160x90.png',
        name: 'example 1',
        price: 10
    },
    {
        id: 3,
        image: 'https://via.placeholder.com/160x90.png',
        name: 'example 1',
        price: 10
    },
    {
        id: 4,
        image: 'https://via.placeholder.com/160x90.png',
        name: 'example 1',
        price: 10
    },
    {
        id: 5,
        image: 'https://via.placeholder.com/160x90.png',
        name: 'example 1',
        price: 10
    },
    {
        id: 6,
        image: 'https://via.placeholder.com/160x90.png',
        name: 'example 1',
        price: 10
    },
    {
        id: 7,
        image: 'https://via.placeholder.com/160x90.png',
        name: 'example 1',
        price: 10
    },
    {
        id: 8,
        image: 'https://via.placeholder.com/160x90.png',
        name: 'example 1',
        price: 10
    },
    {
        id: 9,
        image: 'https://via.placeholder.com/160x90.png',
        name: 'example 1',
        price: 10
    },
    {
        id: 10,
        image: 'https://via.placeholder.com/160x90.png',
        name: 'example 1',
        price: 10
    },
];

const updateProductsCount = (value: number) => {
    emit('on-change-products-count', value);
}
</script>

<template>
    <div class="row text-center">
        <div class="col-12 text-center">
            <h2>Feature product</h2>
        </div>
    </div>
    <div class="row">
        <ProductItem v-for="product in products" :product="product" @on-change-products-count="updateProductsCount" />
    </div>
</template>
