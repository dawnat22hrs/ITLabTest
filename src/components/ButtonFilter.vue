<script setup>
import { ref } from 'vue';

//state
const areFilterCategoriesVisible = ref(false)

const emits = defineEmits(['select'])
defineProps({
    filterCategories: Array,
})

//methods
const selectFilterCategory = (name) => {
    emits('select', name)
    areFilterCategoriesVisible.value = false
}
</script>

<template>
    <div class="block-btn">
        <button 
            class="btn" 
            @click="areFilterCategoriesVisible = !areFilterCategoriesVisible"
        ><slot/></button>
        <ul v-if="areFilterCategoriesVisible">
            <li 
                v-for="filterCategory in filterCategories"
                :key="filterCategories.val"
                @click="selectFilterCategory(filterCategory.name)"
            >{{ filterCategory.name }}</li>
        </ul>
    </div>
</template>

<style scoped lang="scss">

.block-btn {
    .btn {
        width: 121.49px;
        height: 36px;
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        border: none;
        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 400;
        font-size: 12px;
        line-height: 15px;
        color: #B4B4B4;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    ul {
        position: relative;
        width: 121.49px;
        top: 0px;
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);            border-radius: 4px;
        border: none;
        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 400;
        font-size: 12px;
        line-height: 15px;
        color: #B4B4B4;
        cursor: pointer;
        //display: none;

        li {
            width: 100%;
            height: 36px;
            border-top: 1px solid gray;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        }
}

</style>