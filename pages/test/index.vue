<template>
  <div class="container">

  </div>
</template>

<script>
  import gsap from 'gsap';
  export default {
    name: 'test-page',
    layout: 'homepage',
    mounted() {
      this.$nextTick(() => {
        //this.moveStack();
      });
    },
    methods: {
      moveStack() {
        const container = document.getElementsByClassName('container')[0];
        const stack = document.getElementsByClassName('card-stack')[0];
        const midPt = {x: container.offsetWidth / 2, y: container.offsetHeight / 2};
        //console.log(stack., stack.);
        gsap.to(stack, {
          left: `${midPt.x - 100}px`,
          top: `${midPt.y - 100}px`,
        })
      }
    }
  }
</script>

<style scoped>
.container {
  width: 50%;
  height: 95vh;
  border: solid 1px red;
}
</style>
