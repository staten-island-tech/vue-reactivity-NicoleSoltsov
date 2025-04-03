<script setup>
</script>

<template>
  <div id="app">
    <header class="app-header">
      <h1>Crepe Maker</h1>
    </header>
    
    <main>
      <router-view />
    </main>

    <footer class="app-footer">
      <p>© 2025 Crepe Maker. All rights reserved.</p>
    </footer>
  </div>
</template>

<style scoped>
h1 {
    text-align: center;
    font-family: "Playfair Display", serif;
    border-radius: 15px;
    display: flex;
    justify-content: center;
    align-items: center;
    line-height: 1; 
    width: 400px;
    height: 70px;
    border-style: solid;
    border-width: 3px;
    border-color: darkmagenta;
    background-color: lightpink;
    margin: auto;
}
#app {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    text-align: center;
    font-family: 'Arial', sans-serif;
}

.app-header {
    background-color: #DAB1DA;
    padding: 35px;
    font-size: 24px;
    font-weight: bold;
    color: #4A2C2A;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

main {
    flex: 1;
    padding: 20px;
}

.app-footer {
    background-color: #FFCC99;
    padding: 10px;
    font-size: 14px;
    color: #4A2C2A;
    box-shadow: 0 -4px 6px rgba(0, 0, 0, 0.1);
}
</style>
