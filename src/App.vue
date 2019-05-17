<template>
  <div id="app">
    <animal-list></animal-list>
    <!-- <natasa></natasa> -->
  </div>
</template>

<script>
import AnimalList from './components/AnimalList.vue'
import Natasa from './components/Natasa.vue'

export default {
  name: 'app',
  components: {
    AnimalList,
    Natasa
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
