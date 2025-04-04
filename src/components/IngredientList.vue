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
    flex-wrap: wrap;  /* Allows wrapping to the next line */
    gap: 10px;        /* Adds spacing between items */
    justify-content: flex-start; /* Aligns items to the start of the row */
    padding: 20px;
    width: 100%;  /* Ensures it takes the full width of its parent */
    box-sizing: border-box; /* Ensures padding/borders are included in width */
}

/* Ensure the items take up flexible space */
.ingredient-list > .ingredient-item {
    flex: 1 1 180px; /* Makes the items flexible, 180px is the minimum width */
    box-sizing: border-box; /* Ensures padding/borders are included in width */
}
</style>
