<script setup>
const emit = defineEmits(["category"])

const categories = [
"all",
"mobile",
"electronics",
"fashion"
]
</script>

<template>
<div class="category-list">
<h3>Categories</h3>

<button
v-for="cat in categories"
:key="cat"
@click="emit('category',cat)"
>
{{cat}}
</button>

</div>
</template>

<style scoped>
.sidebar-card {
  background: white;
  padding: 20px;
  border-radius: 12px;
  border: 1px solid #eee;
  box-shadow: 0 4px 6px rgba(0,0,0,0.02);
}

h3 {
  margin-bottom: 15px;
  font-size: 1.1rem;
  color: #333;
}

.category-list {
  display: flex;
  flex-direction: column; /* Stack vertically */
  gap: 8px;
}

button {
  text-align: left;
  padding: 10px 15px;
  border: 1px solid transparent;
  background: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 0.95rem;
  color: #555;
}

button:hover {
  background-color: #f0f4ff;
  color: #3498db;
}

/* Highlight the selected button */
button.active {
  background-color: #3498db;
  color: white;
  font-weight: bold;
}
</style>
