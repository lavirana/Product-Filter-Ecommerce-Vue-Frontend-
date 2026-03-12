<script setup>
import { ref, computed } from 'vue'
import { products } from './data/products'

import ProductList from './components/ProductList.vue'
import FiltersSidebar from './components/FiltersSidebar.vue'
import SearchBar from './components/SearchBar.vue'

const search = ref("")
const category = ref("all")
const sortBy = ref("") 
const priceRange = ref({ min: 0, max: 5000 })

// Functions to update state when children emit events
function updateSearch(value) {
  search.value = value
}
function updatePrice(value) {
  priceRange.value = value
}
function updateSort(value) {
  sortBy.value = value
}
function updateCategory(value) {
  category.value = value
}

const filteredProducts = computed(() => {
  // STEP 1: Filter the products first
  let result = products.filter(product => {
    const matchCategory = category.value === "all" || product.category === category.value
    const matchSearch = product.title.toLowerCase().includes(search.value.toLowerCase())
    const matchPrice = product.price >= priceRange.value.min && product.price <= priceRange.value.max

    return matchCategory && matchSearch && matchPrice
  })

  // STEP 2: Sort the filtered results
  // We use [...result] to avoid mutating the original array directly
  if (sortBy.value === "price_low") {
    result.sort((a, b) => a.price - b.price)
  } else if (sortBy.value === "price_high") {
    result.sort((a, b) => b.price - a.price)
  } else if (sortBy.value === "rating") {
    result.sort((a, b) => b.rating - a.rating)
  }

  return result
})
</script>

<template>
  <div class="container">
    <header class="store-header">
      <h1>Ecommerce Store</h1>
      <SearchBar @search="updateSearch" @sort="updateSort" />
    </header>

    <main class="layout">
      <aside class="sidebar">
        <FiltersSidebar @category="updateCategory" @price="updatePrice"/>
      </aside>

      <section class="content">
        <p class="results-count">Showing {{ filteredProducts.length }} products</p>
        <ProductList :products="filteredProducts"/>
      </section>
    </main>
  </div>
</template>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 50px 20px;
}
h1 {
  font-size: 2.5rem;
  font-weight: 800;
  margin-bottom: 30px;
  color: #2c3e50;
}
.store-header {
  margin-bottom: 40px;
  text-align: center;
}
.layout {
  display: grid;
  grid-template-columns: 250px 1fr;
  gap: 30px;
  align-items: start;
}
.sidebar {
  position: sticky;
  top: 20px;
  background: #f9f9f9;
  padding: 20px;
  border-radius: 12px;
  border: 1px solid #eee;
}
.results-count {
  margin-bottom: 15px;
  color: #666;
  font-weight: 500;
}

@media (max-width: 768px) {
  .layout {
    grid-template-columns: 1fr;
  }
  .sidebar {
    position: static;
  }
}
</style>