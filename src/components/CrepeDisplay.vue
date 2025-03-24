<script setup>
import { computed } from "vue";
import ingredientImages from "@/assets/ingredientsImages.js"; // Import image mapping

// Import static images
const emptyCrepeImage = new URL('@/assets/images/empty-crepe.webp', import.meta.url).href;
const fallbackImage = new URL('@/assets/images/fallback.png', import.meta.url).href;

defineProps(["selectedIngredients"]);

// Function to get ingredient image from mapping
const getImagePath = (ingredient) => ingredientImages[ingredient] || fallbackImage;

// Random positioning for ingredients
const getRandomPosition = () => {
  const randomX = Math.random() * 250;
  const randomY = Math.random() * 250;
  return { left: `${randomX}px`, top: `${randomY}px` };
};  
</script>

<template>
  <div class="crepe-container">
    <div class="crepe">
      <img v-if="selectedIngredients.length === 0" :src="emptyCrepeImage" alt="Empty crepe" class="crepe-base"/>

      <div 
        v-for="(ingredient, index) in selectedIngredients" 
        :key="index" 
        class="ingredient"
        :style="getRandomPosition()">
        <img :src="getImagePath(ingredient)" :alt="ingredient" />
      </div>
    </div>

    <p v-if="selectedIngredients.length === 0" class="empty-message">Your crepe is empty!</p>
  </div>
</template>

<style scoped>
.crepe-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px;
}

.crepe {
    position: relative;
    width: 300px;
    height: 300px;
    background-color: #FFDDC1;
    border-radius: 50%;
    border: 4px solid #D4A373;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
}

.crepe-base {
    width: 100%;
    height: auto;
}

.ingredient {
    position: absolute;
    width: 50px;
    height: 50px;
}

.ingredient img {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
}

.empty-message {
    margin-top: 10px;
    font-size: 18px;
    color: gray;
}
</style>
