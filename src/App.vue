<script setup>

import { ref, computed } from 'vue'
import { products } from './data/products'

import ProductList from './components/ProductList.vue'
import FiltersSidebar from './components/FiltersSidebar.vue'
import SearchBar from './components/SearchBar.vue'

const search = ref("")
const category = ref("all")

function updateSearch(value){
 search.value = value
}

function updateCategory(value){
 category.value = value
}

const filteredProducts = computed(()=>{

 return products.filter(product=>{

 const matchCategory =
 category.value === "all" ||
 product.category === category.value

 const matchSearch =
 product.title.toLowerCase()
 .includes(search.value.toLowerCase())

 return matchCategory && matchSearch

 })

})

</script>
<template>
  <div class="container">
    <header class="store-header">
      <h1>Ecommerce Store</h1>
      <SearchBar @search="updateSearch"/>
    </header>

    <main class="layout">
      <aside class="sidebar">
        <FiltersSidebar @category="updateCategory"/>
      </aside>

      <section class="content">
        <p class="results-count">Showing {{ filteredProducts.length }} products</p>
        <ProductList :products="filteredProducts"/>
      </section>
    </main>
  </div>
</template>

<style scoped>
/* 1. Center the whole app */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding-top: 50px; /* Gives space at the very top of the browser */
}
h1 {
  font-size: 2.5rem;
  font-weight: 800;
  margin-bottom: 30px;
  color: #2c3e50;
}

.store-header {
  margin-bottom: 30px;
  text-align: center;
}

/* 2. Advanced Grid Layout */
.layout {
  display: grid;
  grid-template-columns: 250px 1fr; /* Slightly wider sidebar */
  gap: 30px;
  align-items: start; /* Prevents sidebar from stretching weirdly */
}

/* 3. Sticky Sidebar */
.sidebar {
  position: sticky;
  top: 20px; /* Keeps filters visible while scrolling */
  background: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
}

.results-count {
  margin-bottom: 15px;
  color: #666;
  font-weight: 500;
}

/* 4. Responsive Design (Mobile) */
@media (max-width: 768px) {
  .layout {
    grid-template-columns: 1fr; /* Stack on top of each other */
  }
  
  .sidebar {
    position: static; /* Remove sticky on mobile */
  }
}
</style>