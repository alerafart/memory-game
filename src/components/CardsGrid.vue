<template>
  <Timer class="timer" ref="timerTriggerStart" :flipy="flip" :allFound="finished" />
  <div class="cardwrap row row-cols-6 row-cols-md-8 g-3">
    <div class="card" v-for="(card, index) in cards" :key="index">
      <img
        @click="flipCard(card, index), startTimer(), stopTimer()"
        :src="
          card.isFlipped
            ? '../assets/animals/' + card.image
            : '../assets/square.jpg'
        "
        :alt="card.id"
      />
    </div>
  </div>
</template>

<script>
// import { ref } from 'vue';
// const timerTriggerStart = ref(null);
import cardsItems from "../../cardsList";
import Timer from "./Timer.vue";

export default {
  name: "CardsGrid",
  data() {
    return {
      cards: cardsItems.cardsList,
      pairs: [],
      found: [],
      flip: null,
      finished:false
      // loadingTimeOut:1500
    };
  },
  components: {
    Timer,
  },
  methods: {
    // start timer method to send prop to child component in order to start timer on first flip card event
    startTimer() {
      this.flip = true;
    },
    // compares total cards array with found array
    // if all cards found change finished to true which sends info to timer component
    // in order to stop it
    stopTimer() {
      if(this.found.length == this.cards.length) {
        this.finished = true;
        
      }
    },
    // flip 2 cards and compare them
    flipCard(card) {
      console.log("flip called");
      // timerTriggerStart.value.start();
      card.isFlipped = true;
      this.pairs.push(card);
      if (this.pairs.length == 2) {
        console.log(this.pairs[0].image, this.pairs[1].image);
        this.compare(this.pairs[0].image, this.pairs[1].image);
      }
    },
    // method to duplicate items in an array, not used yet
    duplicate(a) {
      a.flatMap((i) => [i, i]);
    },
    // compares 2 flipped cards
    compare(a, b) {
      if (a == b) {
        console.log("match");
        this.found.push(a, b);
        console.log("pairs found" + this.found);
      } else {
        console.log("no match");

        // unflip cards after 1 second
        this.pairs.forEach((card) => {
          setTimeout(() => {
            card.isFlipped = false;
          }, 1500);
        });
      }
      this.pairs = [];
    },
    // shuffle cards method
    shuffle(array) {
      const newArray = [...array];
      const length = newArray.length;

      for (let start = 0; start < length; start++) {
        const randomPosition = Math.floor(
          (newArray.length - start) * Math.random()
        );
        const randomItem = newArray.splice(randomPosition, 1);
        newArray.push(...randomItem);
      }
      return newArray;
    },
  },
  // calls  shuffle function on each reload
  created() {
    this.cards = this.shuffle(this.cards);

    // add a state 'isFlipped to each single card'
    this.cards.forEach((card) => {
      card.isFlipped = false;
    });
  },
};
</script>

<style>
.show {
  display: block;
}
.hidden {
  visibility: hidden;
}
.cardwrap {
  /* background-image: url("../../public/assets/square.jpg"); */
  border: none;
}
.card {
  --bs-card-border-color: none;
}

</style>
