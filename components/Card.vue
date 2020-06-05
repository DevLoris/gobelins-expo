<template>
  <div class="card" v-bind:style="{
    transform: `rotate(${angle}deg)`,
    display: 'block'
  }"></div>
</template>

<script>
  import {randomBetween} from "../utils/helpers";

  export default {
    name: "Card",
    data(){
      return {
        angle: randomBetween(-90, 90),
      }
    }
  }
</script>

<style scoped>
  .card {
    width: 200px;
    height: 200px;
    background: white;
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
    position: absolute;
    display: block;
  }
</style>
