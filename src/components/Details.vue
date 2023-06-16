<template>
    <div v-if="singleProduct">
        <div class="title">View Details</div>
       <p class="productDetail"><p class="productDetails">Name: </p>{{ singleProduct?.title }}</p>
       <p class="productDetail"><p class="productDetails">Price:</p> {{ singleProduct?.price }}</p>
       <p class="productDetail"><p class="productDetails">Rating:</p>  {{ singleProduct?.rating }}</p>
       <p class="productDetail"><p class="productDetails">Description:</p>  {{ singleProduct?.description }}</p>
    </div>
<div v-else>
Loading...
</div>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

const props = defineProps(['id'])
const singleProduct = ref(null)
onMounted(async()=>{
    try {
        const res = await fetch(`https://dummyjson.com/products/${props.id}`)
        const data = await res.json()
        singleProduct.value = data
    } catch (error) {
        
    }
})

onUnmounted(()=>{
    singleProduct.value = null
})
</script>

<style scoped>
.title{
    text-align: center;
    font-size: 20px;
    font-weight: 600;
    margin-bottom: 5px;
}
.productDetail{
    display: flex;
    font-size: 13px;
}
.productDetails{
    font-size: 13.5px;
    font-weight: 500;
    width: 80px;
}
</style>