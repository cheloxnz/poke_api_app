<template>
  <div id="app">
    <Pokemon msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Pokemon from './components/Pokemon.vue'

export default {
  name: 'App',
  components: {
    Pokemon
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
