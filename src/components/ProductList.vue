<script setup>
import ProductCard from './ProductCard.vue';

defineProps({
    products: {
        type: Array,
        required: true
    }
})
</script>

<template>
    <div class="grid">
        <ProductCard 
        v-for="product in products"
        :key="product.id"
        :product="product"
        />
    </div>
</template>

<style scoped>
.grid{
display:grid;
grid-template-columns:repeat(4,1fr);
gap:20px;
}
</style>