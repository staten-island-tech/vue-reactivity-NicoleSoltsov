<script setup>
import { computed } from "vue";
defineProps(["selectedIngredients"]);

const getImagePath = (ingredient) => {
  const extensions = ['png', 'jpg', 'jpeg', 'svg', 'webp', 'avif']; // List of supported extensions

  for (const ext of extensions) {
    try {
      return new URL(`@/assets/ingredientImages/${ingredient}.${ext}`, import.meta.url).href;
    } catch (e) {
      // Continue checking the next extension
    }
  }

  console.error(`Error loading image for ${ingredient}: No valid file found.`);
  return "/src/assets/images/fallback.png"; // Optional fallback image
};


// Random position generator (you can customize this)
const getRandomPosition = () => {
  const randomX = Math.random() * 250; // 250px max for the crepe container
  const randomY = Math.random() * 250; // 250px max for the crepe container
  return { left: `${randomX}px`, top: `${randomY}px` };
};
</script>

<template>
  <div class="crepe-container">
    <div class="crepe">
      <img v-if="selectedIngredients.length === 0" src="@/assets/images/empty-crepe.webp" alt="Empty crepe" class="crepe-base"/>

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
    object-fit: contain; /* Ensures image maintains aspect ratio */
}

.empty-message {
    margin-top: 10px;
    font-size: 18px;
    color: gray;
}
</style>
