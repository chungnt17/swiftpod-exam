<script setup lang="ts">
import ProductItemCart from '@/components/ProductItemCart.vue';
import { reactive, watch } from 'vue';
import { useToast } from 'vue-toastification';
const emit = defineEmits('on-change-products-count');


const toast = useToast();

const products = reactive(JSON.parse(localStorage.getItem('products') || '[]'));

watch(products, () => localStorage.setItem('products', JSON.stringify(products)))

const removeProduct = (id: Number) => {
    const indexProduct = products.findIndex((p: any) => p.id == id)
    if (indexProduct >= 0) {
        products.splice(indexProduct, 1);
        emit('on-change-products-count', -1);
        toast.success('Xoá sản phẩm thành công');
    } else {
        toast.warning('Xoá sản phẩm không thành công');
    }
}

const changeQuantityProduct = (product: any) => {
    products.forEach((p: any) => {
        if (p.id == product.id) {
            if (product.quantity > 0) {
                p.quantity = product.quantity;
            } else {
                p.quantity = 0;
                toast.warning('Số lượng không được phép nhỏ hơn 0');
            }
            return;
        }
    })
}
const total = products.reduce(function (a, b) {
    return a + b.price * b.quantity;
}, 0);
</script>

<template>
    <div class="row text-center">
        <div class="col-12 d-flex justify-content-between mb-3">
            <h2>Cart</h2>
            <button class="btn btn-primary">Check out</button>
        </div>
    </div>
    <div class="row">
        <table>
            <ProductItemCart v-for="product in products" :product="product"
                @on-change-quantity-product="changeQuantityProduct" @on-remove-product="removeProduct" />
        </table>
        <div class="text-right font-weight-bold w-100 pr-5">Total {{total}}$</div>
    </div>
    <div class="row">
        <div class="col-12 text-right">
            <button class="btn btn-primary">Check out</button>
        </div>
    </div>
</template>
<style scoped>
table {
    width: 100%;
}
</style>
