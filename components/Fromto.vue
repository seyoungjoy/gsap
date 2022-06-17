<!-- Please remove this file from your project -->
<template>
  <section class="container">
    <div class="row">
      <div class="col-12">
        <div class="card"
             v-for="(card, i) in cards"
             :key="card.id"
             ref="cards"
             @click="simpleFade(i)">
          <div class="card-inner">
            <div class="card-name">{{ card.name }}</div>
          </div>
      </div>
    </div>
    </div>
  </section>
</template>

<script>
import { gsap } from 'gsap';

const myCards = [
  {
    id: 0,
    name: 'Prima carta',
  },
  {
    id: 1,
    name: 'Seconda carta',
  },
  {
    id: 2,
    name: 'Terza carta',
  },
  {
    id: 3,
    name: 'Quarta carta',
  }
];
export default {
  name: 'TarocchiCards',
  data() {
    return {
      cards: myCards,
    };
  },
  methods: {
    simpleFade(i) {
      // gsap.fromTo(this.$refs.cards[i],
      //   { opacity:1 },
      //   { opacity:0.5, duration: 1, ease:"elastic"}
      // );
      gsap.fromTo(this.$refs.cards[i],
        { x:0, y:0 },
        { x:100, y:200, duration: 3, ease:"elastic"}
      );
    }
  },
}
</script>
