<script setup>
import ingredientImages from '@/assets/ingredientsImages';

defineProps(['name']);
</script>

<template>
  <div class="box">
    <img :src="ingredientImages[name]" :alt="name" />
    <div>
      <p class="text">{{ name }}</p>
    </div>
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
    height: 300px;
    margin-top: 35px;
    margin-left: 35px;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.box img {
    width: 80%;
    height: auto;
    border: 3px solid #FF87AB;
    margin-top: 10px;
}

.text {
    margin-top: 10px;
    font-family: "Patrick Hand", cursive;
    font-size: 30px;
    color: darkmagenta;
}
</style>
