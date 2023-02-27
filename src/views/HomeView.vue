<script setup>
import { ref } from 'vue';
import ButtonFilter from '../components/ButtonFilter.vue';
import FormAddProduct from '../components/FormAddProduct.vue';
import ProductList from '../components/ProductList.vue';

//state
const parseStorsge = JSON.parse(localStorage.getItem('products')) || []
const products = ref(parseStorsge)

//methods
const saveProductInLS = () => localStorage.setItem('products', JSON.stringify(products.value))

const getProduct = (value) => {
  products.value.push({id: products.value.length, name: value.name, desc: value.desc, link: value.link, price: value.price})
  saveProductInLS()
}

const deleteProduct = (id) => {
  products.value = products.value.filter(x => x.id !== id)
  saveProductInLS()
}
</script>

<template>
  <div class="container">
    <header class="header">
      <h2 class="title">Добавление товара</h2>
      <ButtonFilter/>
    </header>
    <main class="main">
      <FormAddProduct @on-get-product="getProduct"/>
      <ProductList 
        :products="products" 
        @on-delete-product="deleteProduct"
      />
    </main>
  </div>
</template>
 
<style scoped lang="scss">
@import '../assets/scss/fonts.scss';

.header {
  margin-bottom: 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;

  .title {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;
    color: #3F3F3F;
  }
}

.main {
  display: flex;
}
</style>