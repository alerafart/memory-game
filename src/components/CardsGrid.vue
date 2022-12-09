<template>
  <div class=" cardwrap row row-cols-5 row-cols-md-5 g-0">  
    <div class="card" @click="handleClick" v-for="(card, index) in cards" :key="card[index]">
      <img  @click="flipCard(card, card.image)"
        :src= " card.isFlipped ?'../assets/animals/' + card.image : '../assets/square.jpg'"
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
      cards: cardsItems.cardsList
    };
  },
  // props: ["turn", "pic"],
  // created() {
  //   this.cards.forEach((card) => {
  //     card.isFlipped = false;
  //   });
  // },
  methods: {
    flipCard(card) {
      card.isFlipped = true;
    }
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
  background-image: url('../../public/assets/square.jpg');
  border:1px solid black;
}

</style>
