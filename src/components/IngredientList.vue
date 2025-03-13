<script setup>
import IngredientItem from './IngredientItem.vue';
import ingredientImages from '@/assets/ingredientImages.js';

// Get ingredient names dynamically from ingredientImages.js
const ingredients = Object.keys(ingredientImages);
</script>

<template>
  <div class="ingredient-list">
    <IngredientItem v-for="ingredient in ingredients" :key="ingredient" :name="ingredient" />
  </div>
</template>

<style scoped>
.ingredient-list {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
    padding: 20px;
}
</style>
