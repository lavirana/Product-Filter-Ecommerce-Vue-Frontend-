<script setup>
defineProps({
    product: {
        type: Object,
        required: true
    }
})
</script>

<template>
<div class="product-card">
<img :src="product.image">
<h3>{{ product.title }}</h3>
<p>${{product.price}}</p>
<p>⭐ {{product.rating}}</p>
</div>
</template>

<style scoped>
.product-card{
border:1px solid #eee;
padding:15px;
border-radius:8px;
transition:0.3s;
}

.product-card:hover{
box-shadow:0 5px 15px rgba(0,0,0,0.1);
}
/* In your ProductList or ProductCard component */
.product-card {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.product-card:hover {
  transform: translateY(-5px); /* Card lifts up slightly */
  box-shadow: 0 10px 20px rgba(0,0,0,0.1);
}

img {
  border-radius: 8px; /* Round the image corners */
  background-color: #f4f4f4;
}
</style>