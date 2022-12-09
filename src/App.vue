<template>
  <h1>Welcome to the Memory Game</h1>
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <!-- <p>composant avec data venant du parent</p> -->
  <!-- <CardsGrid 
  :turn="handleClick"
  v-for="(card, index) in cards" 
  :key="card[index]"
  :pic="'./assets/animals/' + card.image"/> -->

  <p>composant avec data dedans</p>
  <CardsGrid />
</template>

<script>
import cardsItems from '../cardsList';
import CardsGrid from './components/CardsGrid.vue';
export default {
  name: 'App',
  components: {
    CardsGrid
  },
  data() {
    return {
      cards:cardsItems.cardsList
    };
  },
  methods: {
    handleClick(e) {
      // let clicked = e.target;
      console.log('clicked'+e.target.value)
    }
  },
  created() {
    this.cards.forEach((card) => {
      card.isFlipped = false;
    });
  },
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
