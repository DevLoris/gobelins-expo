<template>
  <nuxt-link :to="this.link" @click.native="unfold($event)" :style="{
    transform: `translate(${this.x}px, ${this.y}px)`,
  }">
    <Card />
    <Card />
    <Card />
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
        link: String,
      },
      methods: {
        unfold(e) {
          const parent = e.target.parentNode;
          const pos = this.getPos();
          const cards = document.getElementsByClassName('card')
          const stack = document.getElementsByClassName('card-stack')[0];
          const container = document.getElementsByClassName('container')[0];
          const midPt = {x: container.offsetWidth / 2, y: container.offsetHeight / 2};

          if(parent.classList.contains('unfolded')) return;
          parent.classList.add('unfolded');
          const tl = gsap.timeline();

          tl.to(stack, {
            x: `${midPt.x - 100}px`,
            y: `${midPt.y - 100}px`,
          });

          tl.to(stack, {
            x: '0px',
            y: '0px',
          })

          for(let i = 0; i <= pos.length - 1; i++ ) {
            tl.to(cards[i], {
              x: `${pos[i].x}px`,
              y: `${pos[i].y}px`,
              rotate: `${randomBetween(-5, 5)}`,
            })
          }
        },
        getPos() {
          let space = 200;
          let stack = 598;
          let pos = [];
          for(let i = 1; i <= 6; i++) {
            let x = i%2 === 0 ? stack / 3 * 2  - 100 : stack / 3 - 100;
            let y = i%2 !== 0 && i !== 1 ? space += space - 100 : space - 100;
            pos.push({x, y});
          }
          return pos;
        }
      },
    }
</script>

<style scoped>
</style>
