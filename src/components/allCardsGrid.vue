<template>
  <div class="cardwrap row row-cols-6 row-cols-md-8 g-3">
    <div class="card"  v-for="(card, index) in selection" :key="index">
      <img @click="flipCard(card, index)"
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
import cardsAll from "../../allCards";
const copy = Object.assign({}, cardsAll.allCards);
const copy2 = Object.assign(copy, cardsAll.allCards)
console.log(copy2);
export default {
  name: "allCardsGrid",
  data() {
    return {
      allCards: cardsAll.allCards,
      selection: [],
      pairs: [],
      found: [],
      // loadingTimeOut: 1500,
    };
  },
  methods: {
    // flip 2 cards and compare them
    flipCard(card) {
      console.log("flip called" + card);
      card.isFlipped = true;
      this.pairs.push(card);
      if (this.pairs.length == 2) {
        console.log(this.pairs[0].image, this.pairs[1].image);
        this.compare(this.pairs[0].image, this.pairs[1].image);
      }
    },
    duplicate(a) {
      a.flatMap((i) => [i, i]);
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
        console.log(this.found);
        this.pairs.forEach((card) => {
          setTimeout(() => {
            card.isFlipped = false;
          }, 1000);
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
    getMultipleRandom(arr, num) {
      let shuffled = [...arr].sort(() => 0.5 - Math.random());
      shuffled.slice(0, num);
      // this.duplicate(shuffled);
      // console.log(shuffled);
      return shuffled;
    },
  },
  // calls  shuffle function on each reload
  onMount() {
    console.log('onMount');
    // this.selection=this.getMultipleRandom(this.allCards, 5)
  },
  calculated: {
    select() {
      let arr = this.allCards;
   arr = this.getMultipleRandom(arr, 4)  ;
    console.log(arr);
    this.allCards=arr;
    }
  },
  // created() {
    
  //   this.selection =JSON.parse(JSON.stringify(this.allCards));
  //   console.log(this.selection);
  //   this.selection = this.shuffle(this.selection);
  //   console.log(this.selection);

  //   this.selection.forEach((card) => {
  //     card.isFlipped = false;
  //   });
  // },
  created() {
    this.allCards.map((item)=> {
      this.selection.push(item);
      // this.selection.push(item,item);
    })
    this.selection =this.selection.flatMap((i) => [i, i]);
    this.selection = this.shuffle(this.selection);
    console.log(this.selection);

    this.selection.forEach((card) => {
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
  /* width: 12rem; */
}
</style>
