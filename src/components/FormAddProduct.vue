<script setup>
import { ref, computed } from 'vue';
import { useVuelidate } from '@vuelidate/core'
import { helpers, required } from '@vuelidate/validators'


const product = ref({
    name: '',
    desc: '',
    link: '',
    price: ''
})

const rules = {
    name: {required},
    link: {required},
    price:{required}
}

/*const rules = computed(() => ({
    product: {
        required: required
    }
}))*/

const v = useVuelidate(rules, {product} /*product.value*/) 
console.log(v)
defineEmits(['onGetProduct'])
</script>

<template>
    <div class="block-add-prod">
        <div class="container__add-prod">
            <div class="inputs__block">
            <div class="name-product product__block">
                <label class="product__label">Наименование товара</label>
                <input class="input" type="text" placeholder="Введите наименование товара" v-model="product.name" />
            </div>
            <div class="desc-product product__block">
                <label class="product__label">Описание товара</label>
                <textarea name="text" placeholder="Введите описание товара" v-model="product.desc"/>
            </div>
            <div class="link-product product__block">
                <label class="product__label">Ссылка на изображение товара</label>
                <input class="input" type="text" placeholder="Введите ссылку" v-model="product.link"/>
            </div>
            <div class="price-product product__block">
                <label class="product__label">Цена товара</label>
                <input class="input" type="text" placeholder="Введите цену" v-model="product.price"/>
            </div>
        </div>
        <button class="btn" @click="$emit('onGetProduct', product), product={} ">Добавить товар</button>
        </div>
    </div>
</template>

<style scoped lang="scss">
.block-add-prod {
    width: 332px;
    height: 440px;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    position: fixed;

    .container__add-prod {
        width: 284px;
        margin: 24px
    }

    

    .inputs__block {
        display: grid;
        grid-template-rows: repeat(4);
        gap: 16px;

        .product__block {
            display: flex;
            flex-direction: column;

            .product__label {
                margin-bottom: 4px;
                font-style: normal;
                font-weight: 400;
                font-size: 10px;
                line-height: 13px;
                letter-spacing: -0.02em;
                color: #49485E;
            }

            .input {
                font-style: normal;
                font-weight: 400;
                font-size: 12px;
                line-height: 15px;
                color: #B4B4B4;

                background: #FFFEFB;
                box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
                border-radius: 4px;
                border: none;
                height: 36px;
                width: 284px;
                display: flex;
                align-items: center;
                padding: 0 16px 0 16px;
                box-sizing: border-box;
            }

            textarea {
                resize: none;
                height: 108px;
                width: 284px;

                font-style: normal;
                font-weight: 400;
                font-size: 12px;
                line-height: 15px;
                color: #B4B4B4;

                background: #FFFEFB;
                box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
                border-radius: 4px;
                border: none;
                display: flex;
                align-items: center;
                padding: 10px 16px 0 16px;
                box-sizing: border-box;
            }
        }
    }
    
    .btn {
        margin-top: 24px;
        width: 284px;
        height: 36px;
        background: #EEEEEE;
        border-radius: 10px;
        border: none;
        font-style: normal;
        font-weight: 600;
        font-size: 12px;
        line-height: 15px;
        text-align: center;
        letter-spacing: -0.02em;
        color: #B4B4B4;
    }
}

@media only screen and (max-width: 390px) {
    .block-add-prod {
        position: absolute;
        
    }
}
</style>