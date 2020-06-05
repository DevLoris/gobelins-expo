<template>
</template>

<script>
  import gsap from 'gsap';
  export default {
    name: 'test-page',
    layout: 'homepage',
    mounted() {
      this.$nextTick(() => {
        this.moveStack();
      });
    },
    methods: {
      moveStack() {
        const stack = document.getElementsByClassName('card-stack')[0];
        stack.style.width = '50%';
        stack.style.height = '95vh';
        //stack.style.transform = 'translate(0px, 0px)';

        /*

        const container = document.getElementsByClassName('container')[0];
        const midPt = {x: container.offsetWidth / 2, y: container.offsetHeight / 2};
        //console.log(stack., stack.);
        gsap.to(stack, {
          x: `${midPt.x - 100}px`,
          y: `${midPt.y - 100}px`,
        })*/
      }
    }
  }
</script>

<style scoped>

</style>
