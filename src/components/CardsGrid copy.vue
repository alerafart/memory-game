<template>
    <Timer ref="timerTriggerStart" :start="start"/>
    <div class="cardwrap row row-cols-6 row-cols-md-8 g-3">
      <div class="card"  v-for="(card, index) in cards" :key="card[index]">
        <img
          @click="flipCard(card, card.id)"
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
import cardsItems from "../../cardsList";
import Timer from './Timer.vue';
// const timerTriggerStart = ref(null);
  export default {
    
    name: "CardsGrid",
    data() {
      return {
        cards: cardsItems.cardsList,
        pairs: [],
        found: [],
        loadingTimeOut:1500
      };
    },
    components:{
      Timer
    },
    props:['start'],
    methods: {
      // flip 2 cards and compare them
      flipCard(card) {
        console.log('flip called');
        // timerTriggerStart.value.start();
        card.isFlipped = true;
        this.pairs.push(card);
        if (this.pairs.length == 2) {
          console.log(this.pairs[0].image, this.pairs[1].image);
          this.compare(this.pairs[0].image, this.pairs[1].image);
        }
      },
      duplicate(a) {
        a.flatMap(i => [i,i]);
        // return a;
      //   a.forEach((card)=>{
      //     a.push(card);
      //     console.log(this.cards);
      //   })
      }, 
      // compares 2 flipped cards
      compare(a, b) {
        if (a == b) {
          console.log("match");
          this.found.push(a, b);
          console.log("pairs found" + this.found);
        } else {
          console.log("no match");

          this.pairs.forEach((card) => {
            setTimeout(() => {
              card.isFlipped = false;
            }, this.loadingTimeOut); 
            
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
    onMount() {
      // this.cards.forEach((card) => {
      //   this.cards.push(card);
      // });
    },
    created() {
      this.cards = this.shuffle(this.cards);
  
      this.cards.forEach((card) => {
        // this.cards.push(card);
        // this.duplicate(card);
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
  .card{
    --bs-card-border-color: none;
    /* width: 12rem; */
  }
  </style>