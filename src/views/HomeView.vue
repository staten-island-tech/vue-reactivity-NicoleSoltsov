<script setup>
import { ref } from 'vue';
import IngredientList from '@/components/IngredientList.vue';
import CrepeDisplay from '@/components/CrepeDisplay.vue';
import CrepeControls from '@/components/CrepeControls.vue';

const selectedIngredients = ref([]);

// Add ingredient without checking for duplicates
const addToCrepe = (ingredient) => {
  selectedIngredients.value.push(ingredient);
};

// Remove the last added ingredient
const removeFromCrepe = () => {
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
        <IngredientList />
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
          @remove-ingredient="removeFromCrepe"
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
    margin-bottom: 20px;
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
