<template>
  <nuxt-link to="/test" @click.native="unfold" :style="{
    transform: `translate(${this.x}px, ${this.y}px)`,
  }">
    <Card />
    <Card />
    <Card />
  </nuxt-link>
</template>

<script>
    import gsap from "gsap";
    import {randomBetween} from "../utils/helpers";
    import Card from "./Card";

    export default {
      name: 'CardStack',
      components: {
        Card,
      },
      props: {
        x: Number,
        y: Number,
      },
      methods: {
        unfold() {
          const pos = this.getPos();
          const cards = document.getElementsByClassName('card')
          const stack = document.getElementsByClassName('card-stack')[0];

          stack.style.transform = 'translate(Opx, 0px)';

          for(let i = 0; i <= pos.length - 1; i++ ) {
            gsap.to(cards[i], {
              x: `${pos[i].x}px`,
              y: `${pos[i].y}px`,
              rotate: `${randomBetween(-5, 5)}`,
            })
          }
        },
        getPos() {
          let space = 200;
          let pos = [];
          for(let i = 1; i <= 3; i++) {
            let x = i%2 === 0 ? 100 / 3 * 2 : 100 / 3;
            let y = i%2 !== 0 && i !== 1 ? space += space : space;
            pos.push({x, y});
          }
          return pos;
        }
      },
    }
</script>

<style scoped>
</style>
