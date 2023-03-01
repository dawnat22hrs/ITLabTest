<script setup>
import { ref } from 'vue';
import ButtonFilter from '../components/ButtonFilter.vue';
import FormAddProduct from '../components/FormAddProduct.vue';
import ProductList from '../components/ProductList.vue';
import vAutoAnimate from '@formkit/auto-animate'

//state
const parseStorsge = JSON.parse(localStorage.getItem('products')) || []
const products = ref(parseStorsge)
const productsSorted = ref([])
const isLoading = ref(false)
const defButton = ref('По умолчанию')
const filterCategories = ref([
  {name: 'По умолчанию', val: 1},
  {name: 'От min цены', val: 2},
  {name: 'От max цены', val: 3},
  {name: 'По названию', val: 4},
])

//methods
const saveProductInLS = () => localStorage.setItem('products', JSON.stringify(products.value))

const getProduct = (value) => {
  isLoading.value = true
  products.value.push({id: products.value.length, name: value.name, desc: value.desc, link: value.link, price: value.price})
  saveProductInLS()
  isLoading.value = false
}

const deleteProduct = (id) => {
  products.value = products.value.filter(x => x.id !== id)
  saveProductInLS()
}

const filteredCategories = ()=> {
  if(productsSorted.value.length){
    return productsSorted.value
  }
}

const filterCategoriesSelect = (name) => {
  defButton.value = name
  productsSorted.value = []
  if(name == 'По названию'){
    productsSorted.value.push(products.value.sort(function(a,b){
      if(a['name']<b['name']) return -1
    }))
    filteredCategories()
  } else if(name == 'От min цены'){
    productsSorted.value.push(products.value.sort(function(a,b){
      if(Number(a['price'])<Number(b['price'])) return -1
    }))
    filteredCategories()
  }else if(name == 'От max цены'){
    productsSorted.value.push(products.value.sort(function(a,b){
      if(Number(a['price'])>Number(b['price'])) return -1
    }))
    filteredCategories()
  } else {
    productsSorted.value.push(products.value.sort(function(a,b){
      if(Number(a['id'])<Number(b['id'])) return -1
    }))
  }
}
</script>

<template>
  <div class="container">
    <header class="header">
      <h2 class="title">Добавление товара</h2>
      <ButtonFilter  v-auto-animate
        :filterCategories="filterCategories"
        @select="filterCategoriesSelect"
      >{{ defButton }}</ButtonFilter>
    </header>
    <main class="main">
      <FormAddProduct @on-get-product="getProduct"/>
      <div class="loading" v-if="isLoading">Loading...</div>
      <ProductList 
        v-else
        v-auto-animate
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
  

  .loading {
    margin: 20vh 60vw;
  }
}
</style>