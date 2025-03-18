<script setup>
import { computed } from "vue";

defineProps(["selectedIngredients"]);

const getImagePath = (ingredient) => {
  return new URL(`/src/assets/ingredientImages/${ingredient}.png`, import.meta.url).href;
};
</script>

<template>
  <div class="crepe-container">
    <div class="crepe">
      <img v-if="selectedIngredients.length === 0" src="@/assets/images/empty-crepe.webp" alt="Empty crepe" class="crepe-base"/>

      <div v-for="(ingredient, index) in selectedIngredients" :key="index" class="ingredient">
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
    width: 100%;
    height: auto;
}

.empty-message {
    margin-top: 10px;
    font-size: 18px;
    color: gray;
}
</style>
