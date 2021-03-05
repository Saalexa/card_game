<template>
  <div class="header">
    <img :src="require('@/assets/images/splendex-logo.svg')">
<!--    <div class="headerCenter" :hidden="!isplay">
      <span>Deck size:</span>
      <select v-model="deckSize">
        <option v-for="index in 8" :key="index">{{ index + 2 }}</option>
      </select>
      <button class="orangeButton" @click="startGame()">Start new game</button>
    </div>-->
    <div class="filler"></div>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    isplay: Boolean,
  },
  data: () => {
    return {
      deckSize: 3,
    }
  },
  methods: {
    startGame: function () {
      this.$parent.$emit('startGame', this.deckSize)
    }
  }
}
</script>

<style scoped>

</style>