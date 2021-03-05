<template>
  <div class="card" @click="flipHandler()">
    <div class="card cardClosed" v-if="!card.isFlipped"></div>
    <div class="card cardOpen" :class="{'bgWhite':!card.matched, 'matched':card.matched}" v-else><img :src="card.url"></div>
  </div>
</template>

<script>
export default {
  name: "Card",
  mounted() {
    this.$on('cardMatched', function() {

    });
  },
  props: {
    card: Object,
  },
  data: () => {
    return {

    }
  },
  methods: {
    flipHandler: function () {
      if (!this.card.isFlipped && !this.card.matched) {
        this.$parent.$emit('cardOpen', this.card)
      }
    }
  }
}
</script>

<style scoped>

</style>