<script setup lang="ts">
import CartIcon from '@/components/icons/Cart.vue';
import { useToast } from "vue-toastification";
const emit = defineEmits('on-change-products-count');

const toast = useToast();

const { product } = defineProps<{
    product: {
        id: Number,
        image: String,
        name: String,
        price: Number;
    }
}>()

const addToCart = () => {
    let products = JSON.parse(localStorage.getItem('products') || '[]');
    let check = false;
    products.forEach((p: any) => {
        if (p.id == product.id) {
            check = true;
            p.quantity++;
            toast.warning('Sản phẩm đã tồn tại trong giỏ hàng.');
            return;
        }
    })
    if (!check) {
        products.push({
            ...product,
            quantity: 1
        });
        emit('on-change-products-count', 1);
        toast.success('Thêm sản phẩm vào giỏ hàng thành công.');
    }
    localStorage.setItem('products', JSON.stringify(products));
}
</script>

<template>
    <div class="col-2 col-md-4 pb-4">
        <div class="product-detail border p-2">
            <img :src="product.image" alt="" width="160" height="90" class="mb-2" />
            <div class="d-flex justify-content-between">
                <div>
                    <div class="price">{{ product.price }}$</div>
                    <div>{{ product.name }}</div>
                </div>
                <div>
                    <button class="btn btn-primary btn-sm" @click="addToCart()">
                        <CartIcon fill="#fff" width="18" height="18" />
                        Add
                    </button>
                </div>
            </div>
        </div>

    </div>
</template>

<style scoped>
img {
    width: 100%;
    height: auto;

}

.price {
    color: #f00;
}
</style>
