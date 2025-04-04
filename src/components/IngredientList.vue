<script setup>
import IngredientItem from './IngredientItem.vue';
import ingredientImages from '@/assets/ingredientsImages.js';

const emit = defineEmits(['add-ingredient', 'remove-ingredient']);

// Get ingredient names dynamically from ingredientImages.js
const ingredients = Object.keys(ingredientImages);
</script>

<template>
  <div class="ingredient-list">
    <IngredientItem 
      v-for="ingredient in ingredients" 
      :key="ingredient" 
      :name="ingredient"
      @add-ingredient="emit('add-ingredient', ingredient)"
      @remove-ingredient="emit('remove-ingredient', ingredient)"
    />
  </div>
</template>

<style scoped>
.ingredient-list {
    display: flex;
    flex-wrap: wrap; 
    gap: 10px;      
    justify-content: flex-start; 
    padding: 20px;
    width: 100%;  /* Ensure it takes the full width of its parent */
    box-sizing: border-box; /* Prevent padding/borders from affecting width */
}

/* Ensure the ingredients take up equal space in a row */
.ingredient-list > .ingredient-item {
    width: calc(50% - 10px);  /* 2 per row, accounting for 10px gap */
    min-width: 180px; /* Prevents it from shrinking too much */
    box-sizing: border-box; /* Ensures padding/borders are included in width */
}
</style>
