<template>
  <div class="cardwrap row row-cols-5 row-cols-md-5 g-0">
    <div class="card" v-for="(card, index) in cards" :key="card[index]">
      <img
        @click="flipCard(card, card.image)"
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
import cardsItems from "../../cardsList";
export default {
  name: "CardsGrid",
  data() {
    return {
      cards: cardsItems.cardsList,
      pairs: [],
      found: [],
    };
  },
  methods: {
    flipCard(card) {
      card.isFlipped = true;
      this.pairs.push(card);
      if (this.pairs.length == 2) {
        console.log(this.pairs[0].image, this.pairs[1].image);
        this.compare(this.pairs[0].image, this.pairs[1].image);
      }
    },
    compare(a, b) {
      if (a == b) {
        console.log("match");
        this.found.push(a, b);
        console.log("pairs found" + this.found);
      } else {
        console.log("no match");
        this.pairs.forEach((card) => {
          setTimeout(()=> {
            card.isFlipped = false;
          }, "2000")
          
        });
      }
      this.pairs = []
    },
    shuffle() {},
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
  background-image: url("../../public/assets/square.jpg");
  border: 1px solid black;
}
</style>
