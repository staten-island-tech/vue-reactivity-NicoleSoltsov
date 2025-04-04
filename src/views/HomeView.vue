<script setup>
import { ref } from 'vue';
import IngredientList from '@/components/IngredientList.vue';
import CrepeDisplay from '@/components/CrepeDisplay.vue';
import CrepeControls from '@/components/CrepeControls.vue';

const selectedIngredients = ref([]);

// Add an ingredient
const addToCrepe = (ingredient) => {
  selectedIngredients.value.push(ingredient);
};

// Remove the last added instance of a specific ingredient
const removeFromCrepe = (ingredient) => {
  const index = selectedIngredients.value.lastIndexOf(ingredient);
  if (index !== -1) {
    selectedIngredients.value.splice(index, 1);
  }
};

// Remove the last ingredient regardless of type (for CrepeControls)
const removeLastIngredient = () => {
  selectedIngredients.value.pop();
};
</script>

<template>
  <div class="home-container">
    <!-- Title -->
    <h1 class="title">Create Your Dream Crepe</h1>
    
    <!-- Main Layout -->
    <div class="content">
      <!-- Left: Ingredient Selection -->
      <div class="left-panel">
        <IngredientList 
          @add-ingredient="addToCrepe" 
          @remove-ingredient="removeFromCrepe" 
        />
      </div>

      <!-- Center: Crepe Display -->
      <div class="center-panel">
        <CrepeDisplay :selectedIngredients="selectedIngredients" />
      </div>

      <!-- Right: Controls -->
      <div class="right-panel">
        <CrepeControls 
          :selectedIngredients="selectedIngredients"
          @add-ingredient="addToCrepe"
          @remove-ingredient="removeLastIngredient"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.home-container {
    text-align: center;
    padding: 20px;
}

.title {
    font-size: 32px;
    font-weight: bold;
    color: #4A2C2A;
    margin-bottom: 10px;
}

.content {
    display: flex;
    justify-content: space-around;
    align-items: flex-start;
    gap: 20px;
    padding: 20px;
}

.left-panel, .right-panel {
    width: 30%;
}

.center-panel {
    width: 40%;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>
