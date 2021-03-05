<template>
  <div id="app">
    <Header></Header>
    <Rules v-if="!isPlay"></Rules>
    <Playfield v-else></Playfield>
  </div>
</template>

<script>
import Playfield from './components/Playfield.vue'
import Rules from './components/Rules.vue'


export default {
  name: 'App',
  components: {
    Playfield,
    Rules
  },
  data: () => {
    return {
      isPlay: false,
    }
  },
  mounted() {
    this.$on('startGame', function() {
      this.isPlay = true;
    });
  }
}
</script>

<style scoped>
@import './assets/scss/app.css';
</style>
