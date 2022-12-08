<template>
  <h1>Welcome to the Memory Game</h1>
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <CardsGrid :turn="handleClick"/>

</template>

<script>
import CardsGrid from './components/CardsGrid.vue';
export default {
  name: 'App',
  components: {
    CardsGrid
  },
  data() {
    return {
      turned:false
    }
  },
  methods: {
    handleClick(e) {
      // let clicked = e.target;
      console.log('clicked'+e)
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
