<script setup>
import { ref, computed } from "vue";
import ingredientImages from "@/assets/ingredientsImages.js"; // Import image mapping

// Import static images
const emptyCrepeImage = new URL('@/assets/images/empty-crepe.webp', import.meta.url).href;
const fallbackImage = new URL('@/assets/images/fallback.png', import.meta.url).href;

const props = defineProps(["selectedIngredients"]);

// Function to get ingredient image from mapping
const getImagePath = (ingredient) => ingredientImages[ingredient] || fallbackImage;

const ingredientPositions = ref({});

const getIngredientPosition = (ingredient, index) => {
  if (!ingredientPositions.value[index]) {
    const centerX = 150;
    const centerY = 150;
    const maxRadius = 50; // Maximum distance from the center

    const angle = (index * (360 / props.selectedIngredients.length)) * (Math.PI / 180);

    // Calculate raw positions
    let posX = centerX + maxRadius * Math.cos(angle);
    let posY = centerY + maxRadius * Math.sin(angle);

    // Adjust for ingredient size to center the image
    posX -= 50;
    posY -= 50;

    // Make sure the distance from the center does not exceed maxRadius
    const distance = Math.sqrt((posX - centerX) ** 2 + (posY - centerY) ** 2);
    if (distance > maxRadius) {
      const scale = maxRadius / distance;
      posX = centerX + (posX - centerX) * scale;
      posY = centerY + (posY - centerY) * scale;
    }

    ingredientPositions.value[index] = { left: `${posX}px`, top: `${posY}px` };
  }
  return ingredientPositions.value[index];
};

</script>

<template>
  <div class="crepe-container">
    <div class="crepe">
      <!-- Keep the base crepe image -->
      <img :src="emptyCrepeImage" alt="Empty crepe" class="crepe-base"/>

      <!-- Ingredients layered on top -->
      <div 
        v-for="(ingredient, index) in selectedIngredients" 
        :key="index" 
        class="ingredient"
        :style="getIngredientPosition(ingredient, index)">
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
    border-radius: 50%;
    border: 4px solid transparent;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
}

.crepe-base {
    width: 100%;
    height: auto;
    position: absolute; /* Ensures it's always behind ingredients */
    transform: scale(1.7);
}

.ingredient {
    position: absolute;
    width: 50px;
    height: 50px;
}

.ingredient img {
    max-width: 100%;
    max-height: 100%;
    transform: scale(4);
    object-fit: contain;
}

.empty-message {
    margin-top: 10px;
    font-size: 18px;
    color: palevioletred;
}
</style>
