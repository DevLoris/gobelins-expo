<template>
  <div class="homepage">
    <CustomHeader />
    <CardStack :x="200" :y="200" class="card-stack"/>
    <nuxt />
    <Footer />
  </div>
</template>

<script>
import CustomHeader from '~/components/Header.vue'
import Footer from '~/components/Footer.vue'
import CardStack from "../components/CardStack";

export default {
  components: {
    CustomHeader,
    Footer,
    CardStack,
  },
  head () {
    return {
      title: 'Prismic Nuxt.js Multi Page Website',
    }
  },
  // Called before rendering the layout (even for error page)
  async middleware({ store, $prismic }) {
    await store.dispatch('fetchGlobal', $prismic)
  }
}
</script>

<style>
  .homepage {
    height: 100vh;
    background: blue;
  }

  .card-stack{
    position: absolute;
  }

</style>
