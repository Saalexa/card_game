<template>
  <div class="rules">
    <div><h1>Rules:</h1></div>
    <div class="rulesList">
      <ol>
        <li>Present the user with an even number of cards, “face down”.</li>
        <li>When the user clicks a card, “flip it over” and reveal the hidden image</li>
        <li>
          When two cards are revealed:
          <ol type="a">
            <li>If the cards are identical, remove them from play.</li>
            <li>If they are not, flip them back.</li>
          </ol>
        </li>
        <li>The game ends when all the cards are removed.</li>
      </ol>
    </div>
    <button class="orangeButton" @click="startGame()">New game</button>
  </div>

</template>

<script>
export default {
  name: "Rules",
  methods: {
    startGame: function () {
      this.$parent.$emit('startGame')
    }
  }
}
</script>

<style scoped>

</style>