<script setup>
import ingredientImages from '@/assets/ingredientsImages.js';

// Define props and events
defineProps(['selectedIngredients']);
defineEmits(['add-ingredient', 'remove-ingredient']);

// Get ingredient names dynamically from ingredientImages.js
const ingredients = Object.keys(ingredientImages);
</script>

<template>
  <div class="controls-container">
    <h2 class="title">Choose Ingredients</h2>
    
    <!-- Ingredient Buttons -->
    <div class="ingredient-buttons">
      <button 
        v-for="ingredient in ingredients" 
        :key="ingredient" 
        @click="$emit('add-ingredient', ingredient)"
        class="add-button"
      >
        + {{ ingredient }}
      </button>
    </div>

    <!-- Remove Last Ingredient Button -->
    <button 
      v-if="selectedIngredients.length > 0" 
      @click="$emit('remove-ingredient')" 
      class="remove-button"
    >
      Remove Last Ingredient
    </button>
  </div>
</template>

<style scoped>
.controls-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
}

.title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 15px;
}

.ingredient-buttons {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
    margin-bottom: 15px;
}

.add-button, .remove-button {
    padding: 10px 15px;
    font-size: 16px;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    transition: 0.2s;
}

.add-button {
    background-color: #ffcc99;
    color: #4a2c2a;
}

.add-button:hover {
    background-color: #ffb366;
}

.remove-button {
    background-color: #ff6666;
    color: white;
}

.remove-button:hover {
    background-color: #cc3333;
}
</style>
