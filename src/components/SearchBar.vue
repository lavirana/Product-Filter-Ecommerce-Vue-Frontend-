<script setup>
import { ref } from 'vue'

const search = ref("")
const emit = defineEmits(["search"])

// Instead of a watch, we can emit directly on input for better performance
const handleInput = () => {
  emit("search", search.value)
}
</script>

<template>
  <div class="search-wrapper">
    <div class="search-container">
      <span class="search-icon">🔍</span>
      <input
        v-model="search"
        @input="handleInput"
        placeholder="Search for electronics, fashion..."
        class="search-input"
      />
    </div>
  </div>
</template>

<style scoped>
.search-wrapper {
  display: flex;
  justify-content: center;
  margin-bottom: 40px;
}

.search-container {
  position: relative;
  width: 100%;
  max-width: 600px; /* Limits width so it's not too stretched */
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
  padding: 12px 15px 12px 45px; /* Extra left padding for the icon */
  font-size: 1rem;
  border: 2px solid #eee;
  border-radius: 50px; /* Rounded pill shape looks modern */
  outline: none;
  transition: all 0.3s ease;
  box-shadow: 0 2px 5px rgba(0,0,0,0.03);
}

/* Add a nice blue border when user clicks */
.search-input:focus {
  border-color: #3498db;
  box-shadow: 0 4px 12px rgba(52, 152, 219, 0.15);
  background-color: #fff;
}
</style>