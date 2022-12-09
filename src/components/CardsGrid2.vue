<template>
  <div class="row row-cols-5 row-cols-md-5 g-0">
    <!-- <div class="card" v-for="(card, index) in cards" :key="card[index]" @click="turn" >
      <img :src="pic" class="" />
    </div> -->
    <!-- <div class="card">
      <img
        :src="pic"
        class=""
        @click="turn"
      />
    </div> -->
    
    <div class="card" @click="handleClick" v-for="(card, index) in cards" :key="card[index]">
      <img  @click="flipCard(card, card.image)"
        :src="'../assets/animals/' + card.image"
        class=""
        :alt="card.id"
        
      />
    </div>

  </div>
</template>

<script>
import cardsItems from "../../cardsList";

export default {
  name: "CardsGrid2",

  data() {
    return {
      cards: cardsItems.cardsList
    };
  },
  setup() {
    
  },

  props: ["turn", "pic"],
  // created() {
  //   this.cards.forEach((card) => {
  //     card.isFl = false;
  //   });
  // },
  methods: {
    flipCard(card) {
      card.isFlipped = true;
    },
    handleClick(e) {
      let card = e.target;
      console.log(e.target.alt, e.target);
      // this.flipCard(e.target);
      this.flipCard(card);

      // console.log('clicked'+ e.target);
      // console.log('clicked'+ this.cards.card)
    },
  },
};
</script>

<style>
.hidden {
  display: none;
}

</style>
