<script setup>
import CardProduct from './CardProduct.vue'

const emits = defineEmits(['onDeleteProduct'])
defineProps({
    products: Array,
})

//methods
const deleteProduct = (id) => emits('onDeleteProduct', id)
</script>

<template>
    <div class="list">
        <CardProduct 
        v-for="product in products"
        :key="product.id"
        :product="product"
        @on-delete-product="deleteProduct"
        />
    </div>
</template>

<style scoped lang="scss">
.list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
    position:relative;
    left: 348px;
}

@media only screen and (max-width: 390px) {
    .list {
        display: grid;
        grid-template-columns: repeat(1, 1fr);
        gap: 16px;
        position: relative;
        left: 0;
        top: 464px;
    }
}
</style>