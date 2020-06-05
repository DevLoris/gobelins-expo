<template>
  <nuxt-link :to="this.link" @click.native="unfoldEvent($event)" :style="{
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
      mounted() {
          //Si c'est notre route actuellement, on unfold
          if(this.link === $nuxt.$router.currentRoute.fullPath) {
              this.unfold(this.$el, 0.01)
          }

          //Si on revient sur la home, on ferme ce bloc
          $nuxt.$on('routeChanged', (to, from) => {
              if(from.fullPath === this.link && to.fullPath === "/")
                  this.fold(this.$el);
          })
      },
      components: {
        Card,
      },
      props: {
        x: Number,
        y: Number,
        link: String,
        amount: {
            type: Number,
            default: 6
        }
      },
      methods: {
        fold(element) {
            const tl = gsap.timeline();
            const cards = element.getElementsByClassName('card')
            for(let i in cards) {
                tl.to(cards[i], {
                    x: 0,
                    y: 0,
                    rotate: `${randomBetween(-90, 90)}`,
                    duration: 0.3
                })
            }
        },
        unfoldEvent(e) {
            //Si ca provient de l'évent
            this.unfold(e.target.parentNode);
            e.preventDefault()
        },
        unfold(element, unfold_duration = 0.5) {
          const parent = element;
          const pos = this.getPos();
          const cards = element.getElementsByClassName('card')
          const container = document.getElementsByClassName('container')[0];

          if(parent.classList.contains('unfolded')) return;
          parent.classList.add('unfolded');
          const tl = gsap.timeline();


          for(let i = 0; i <= pos.length - 1; i++ ) {
            tl.to(cards[i], {
              x: `${pos[i].x}px`,
              y: `${pos[i].y}px`,
              rotate: `${randomBetween(-10, 10)}`,
                duration: unfold_duration
            })
          }
        },
        getPos() {
          // on calcule les points sur un cercle
          let findPointOnCircle = (originX, originY , radius, angleRadians) => {
              let x = radius * Math.cos(angleRadians) + originX;
              let y = radius * Math.sin(angleRadians) + originY;
              return {x,y}
          };

            let pos = [];
          for(let i = 0; i < this.amount; i++) {
            pos.push(findPointOnCircle(this.x - 200, this.y - 200, 180, (2 * i / this.amount)*Math.PI));
          }
          console.log(pos);
          return pos;
        }
      },
    }
</script>

<style scoped>
</style>
