<script setup>
import { ref } from 'vue'

const search = ref("")
const emit = defineEmits(["search", "sort"]) // Define both emits here

const handleInput = () => {
  emit("search", search.value)
}
</script>

<template>
  <div class="search-bar-layout">
    <div class="search-container">
      <span class="search-icon">🔍</span>
      <input
        v-model="search"
        @input="handleInput"
        placeholder="Search for electronics, fashion..."
        class="search-input"
      />
    </div>

    <div class="sort-container">
      <select class="sort-select" @change="emit('sort', $event.target.value)">
        <option value="">Sort By</option>
        <option value="price_low">Price: Low to High</option>
        <option value="price_high">Price: High to Low</option>
        <option value="rating">Top Rated</option>
      </select>
    </div>
  </div>
</template>

<style scoped>
.search-bar-layout {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px; /* Space between search and sort */
  margin-bottom: 40px;
  width: 100%;
}

.search-container {
  position: relative;
  flex: 1; /* Allows search to take more space */
  max-width: 500px;
}

.search-icon {
  position: absolute;
  left: 15px;
  top: 50%;
  transform: translateY(-50%);
  color: #888;
}

.search-input {
  width: 100%;
  padding: 12px 15px 12px 45px;
  font-size: 1rem;
  border: 2px solid #eee;
  border-radius: 5px;
  outline: none;
  transition: all 0.3s ease;
}

.search-input:focus {
  border-color: #3498db;
  box-shadow: 0 4px 12px rgba(52, 152, 219, 0.1);
}

.sort-select {
  padding: 12px 20px;
  font-size: 1rem;
  border: 2px solid #eee;
  border-radius: 5px; /* Matching the search bar style */
  background-color: white;
  color: #555;
  cursor: pointer;
  outline: none;
  transition: all 0.3s ease;
  margin-left: 30%;
}

.sort-select:hover {
  border-color: #ccc;
}

.sort-select:focus {
  border-color: #3498db;
}

/* For mobile: stack them on top of each other */
@media (max-width: 600px) {
  .search-bar-layout {
    flex-direction: column;
    align-items: stretch;
  }
  
  .search-container {
    max-width: 100%;
  }
}
</style>