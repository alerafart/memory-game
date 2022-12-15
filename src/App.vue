<template>
  <div class="container px-4 text-center">
    <h1>Welcome to the Memory Game</h1>
    <!-- <CardsGrid 
  :turn="handleClick"
  v-for="(card, index) in cards" 
  :key="card[index]"
  :pic="'./assets/animals/' + card.image"/> -->
    <CardsGrid />
    <!-- <allCardsGrid /> -->
    <footer>Thanks for playing</footer>
  </div>
</template>

<script>
// import allCardsGrid from "./components/allCardsGrid.vue";
import CardsGrid from "./components/CardsGrid.vue";

export default {
  name: "App",
  components: {
    CardsGrid,
    // allCardsGrid
  },
  data() {
    return {

    };
  }
};
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
footer {
  padding: 2rem;
  font-size: 1.5rem;
}
</style>
