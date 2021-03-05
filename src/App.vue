<template>
  <div id="app">
    <Header :isplay="isPlay"></Header>
    <Rules v-if="!isPlay"></Rules>
    <Playfield v-else></Playfield>
  </div>
</template>

<script>
import Playfield from './components/Playfield.vue'
import Rules from './components/Rules.vue'
import Header from './components/Header.vue'


export default {
  name: 'App',
  components: {
    Playfield,
    Rules,
    Header
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
  },
  methods: {

  }
}
</script>

<style scoped>
@import './assets/scss/app.css';
</style>
