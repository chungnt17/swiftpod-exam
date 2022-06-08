<script setup lang="ts">
import TrashIcon from '@/components/icons/Trash.vue';
import { reactive } from 'vue';
import { useToast } from "vue-toastification";
const emit = defineEmits(['on-remove-product', 'on-change-quantity-product']);

const toast = useToast();

const props = defineProps<{
    product: {
        id: Number,
        image: String,
        name: String,
        price: Number;
        quantity: Number
    }
}>()

const product = reactive(props.product);

</script>


<template>
    <tr>
        <td>
            <img :src="product.image" alt="" width="160" height="90" class="mb-2" />
        </td>
        <td class="text-left">
            <h4>{{ product.name }}</h4>
            <div class="price">{{ product.price }}$</div>
        </td>
        <td>
            <div>Quantity</div>
            <input class="form-control" type="number" v-model="product.quantity" @change="$emit('on-change-quantity-product', product)">
        </td>
        <td>
            <div>Sub Total</div>
            <div class="price">{{ product.price * product.quantity }}$</div>
        </td>
        <td>
            <button class="p-3 border"><TrashIcon fill="#00f" @click="$emit('on-remove-product', product.id)"/></button>
        </td>
    </tr>
</template>

<style scoped>
tr {
    border: solid 1px #ccc;
}
td:first-child {
    width: 160px;
}
td:nth-child(2) {
    width: 50%;
}
td {
    padding: 5px;
}
img {
    width: 100%;
    height: auto;

}

.price {
    color: #f00;
}
</style>
