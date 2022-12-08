<template>
  <div class="row row-cols-5 row-cols-md-5 g-0">
    <div class="card" v-for="card in cards" :key="card.name">
      <img :src="card.image" class="" @click="turn"/>
    </div>
  </div>
</template>

<script>
import cardsItems from '../../cardsList';
export default {
  name: "CardsGrid",

  data() {
    return {
        cards:cardsItems.cardsList
    };
  },
  props: [
    'turn'
  ],
  methods: {
    // handleClick(e) {
    //   let clicked = e.target.value;
    //   console.log(clicked)
    // }
    // cardList() {
    //     for(let i=0; i<40; i++) {
    //         this.cards.push({ name: i, image: "../assets/animals/" +i +".jpg" },)
    //     }
    // }
  },
};

</script>

<style></style>
