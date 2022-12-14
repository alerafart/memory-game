<template>
  <div class="container px-4 text-center">
    <h1>Welcome to the Memory Game</h1>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <p>composant avec data venant du parent</p> -->
    <!-- <CardsGrid 
  :turn="handleClick"
  v-for="(card, index) in cards" 
  :key="card[index]"
  :pic="'./assets/animals/' + card.image"/> -->
    <!-- <Timer2 /> -->
    <CardsGrid />
    <!-- <allCardsGrid /> -->
  </div>
</template>

<script>
// import cardsItems from "../cardsList";
// import allCardsGrid from "./components/allCardsGrid.vue";
import CardsGrid from "./components/CardsGrid.vue";
// import Timer2 from "./components/Timer2.vue";
export default {
  name: "App",
  components: {
    CardsGrid,
    // Timer2,
    // allCardsGrid
  },
  data() {
    return {
      // cards: cardsItems.cardsList,
    };
  },
  // onMount() {
  //   this.cards.forEach((card) => {
  //     this.cards.push(card);
  //   });
  // },
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
</style>
