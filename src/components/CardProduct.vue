<script setup>
import DeleteIcon from './icons/DeleteIcon.vue';

defineProps({
    product: Object
})

defineEmits(['onDeleteProduct'])
</script>

<template>
    <div class="card-block">
        <img :src="link" alt="product" class="img">
        <div class="card-block__container">
            <h3 class="title__card">{{ product.name }}</h3>
            <p class="desc__card">{{ product.desc }}</p>
            <p class="price__card">{{ product.price }} руб.</p>
        </div>
        <div 
            class="btn-del" 
            @click="$emit('onDeleteProduct', product.id)"
        >
            <DeleteIcon class="icon"/>
        </div>
    </div>
</template>



<style scoped lang="scss">
.card-block {
    width: 332px;
    height: 423px;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    box-sizing: border-box;
    position: relative;

    .btn-del {
        width: 32px;
        height: 32px;
        background: #FF8484;
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
        border-radius: 10px;
        display: flex;
        align-items: center;
        justify-content: center;
        position: absolute;
        left: 308px;
        bottom: 399px;
        cursor: pointer;
        visibility: hidden;
        z-index: -1;
        opacity: 0;

        .icon {
            background: #FF8484;
        }
    }

    .img {
        box-sizing: border-box;
        width: 100%;
        height: 47.285%;
    }

    .card-block__container {
        margin: 16px 16px 24px 16px;

        .title__card {
            font-style: normal;
            font-weight: 600;
            font-size: 20px;
            line-height: 25px;
            color: #3F3F3F;

            margin-bottom: 16px;
        }

        .desc__card {
            font-style: normal;
            font-weight: 400;
            font-size: 16px;
            line-height: 20px;
            color: #3F3F3F;

            margin-bottom: 32px;
        }

        .price__card {
            font-style: normal;
            font-weight: 600;
            font-size: 24px;
            line-height: 30px;
            color: #3F3F3F;
        }
    }
}

.card-block:hover .btn-del{
    visibility: visible;
    z-index: 99;
    opacity: 1;
}

.card-block:hover .icon{
    visibility: visible;
    z-index: 99;
    opacity: 1;
}
</style>