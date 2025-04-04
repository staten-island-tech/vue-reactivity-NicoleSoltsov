<script setup>
import ingredientImages from '@/assets/ingredientsImages';

const props = defineProps(['name']);
const emit = defineEmits(['add-ingredient', 'remove-ingredient']);
</script>

<template>
  <div class="box">
    <img :src="ingredientImages[name]" :alt="name" />
    <p class="text">{{ name }}</p>
    
    <!-- Add and Remove buttons inside the box -->
    <button @click="emit('add-ingredient', name)" class="add-button">+ Add</button>
    <button @click="emit('remove-ingredient', name)" class="remove-button">- Remove</button>
  </div>
</template>

<style scoped>
.box {
    background-color: #FFD0D7;
    border-style: solid;
    border-width: 3px;
    border-color: lightpink;
    justify-content: center;
    overflow: hidden;
    width: 200px;
    height: 320px; /* Reduced height */
    margin-top: 35px;
    margin-left: 35px;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: 10px;
}

.box img {
    width: 80%;
    height: auto;
    border: 3px solid #FF87AB;
    margin-top: 10px;
    background-color: white;
}

.text {
    margin-top: 5px; /* Reduced space */
    margin-bottom: 5px; /* Reduce space below */
    font-family: "Patrick Hand", cursive;
    font-size: 24px; /* Slightly smaller text */
    color: darkmagenta;
}

.add-button, .remove-button {
    margin-top: 5px; /* Reduced space */
    padding: 6px 10px; /* Smaller buttons */
    font-size: 14px; /* Slightly smaller text */
    border: none;
    cursor: pointer;
    border-radius: 5px;
}

.add-button {
    background-color: #ffcc99;
    color: #4a2c2a;
}

.remove-button {
    background-color: #ff6666;
    color: white;
}

.add-button:hover {
    background-color: #ffb366;
}

.remove-button:hover {
    background-color: #cc3333;
}
</style>
