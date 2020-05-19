<template>
  <div id="app">
    <FoodOrder></FoodOrder>
  </div>
</template>

<script>
import FoodOrder from './components/FoodOrder.vue'
export default {
  name: 'App',
  components: {
    FoodOrder
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  padding: 2rem;
}
body{
  background-color: #121212;
}
</style>
