<template>
  <div class="playfield">
    <div class="startScreen" v-if="!isStarted">
      <div>Splendex Memory Game</div>
      <select v-model="deckSize">
        <option v-for="index in 8" :key="index">{{ index + 2 }}</option>
      </select>
      <button @click="startGame()" :disabled="loading">Start new game</button>
    </div>
    <div class="gameScreen" v-else>
      <div class="status">
        <div>Current tries: {{currentStep}}</div>
        <div>Best: {{bestGame}}</div>
        <div><button @click="restartGame()">Restart</button></div>
      </div>
      <div class="cards">
        <Card v-for="(card, index) in cards" :key="index" :card="card"></Card>
      </div>
    </div>

  </div>
</template>

<script>
import _ from 'lodash'
import Card from './Card.vue'

const imgs = [
  {url: require('@/assets/images/cards/angular.png'), name: 'angular', matched: false, isFlipped: false},
  {url: require('@/assets/images/cards/d3.png'), name: 'd3', matched: false, isFlipped: false},
  {url: require('@/assets/images/cards/jenkins.png'), name: 'jenkins', matched: false, isFlipped: false},
  {url: require('@/assets/images/cards/postcss.png'), name: 'postcss', matched: false, isFlipped: false},
  {url: require('@/assets/images/cards/react.png'), name: 'react', matched: false, isFlipped: false},
  {url: require('@/assets/images/cards/redux.png'), name: 'redux', matched: false, isFlipped: false},
  {url: require('@/assets/images/cards/sass.png'), name: 'sass', matched: false, isFlipped: false},
  {url: require('@/assets/images/cards/splendex.png'), name: 'splendex', matched: false, isFlipped: false},
  {url: require('@/assets/images/cards/ts.png'), name: 'ts', matched: false, isFlipped: false},
  {url: require('@/assets/images/cards/webpack.png'), name: 'webpack', matched: false, isFlipped: false}
];

export default {
  name: "Playfield",
  components: {
    Card
  },
  data: () => {
    return {
      isStarted: false,
      deckSize: 3,
      images: [],
      cards: [],
      loading: false,
      openCards: [],
      matchedCards: [],
      currentStep: 0,
      bestGame: 0,
    }
  },
  mounted() {
    this.getImg();
    this.$on('cardOpen', function(card) {
      this.cardOpen(card)
    });
  },
  methods: {
    startGame: function () {
      this.loading = true;
      this.getImg();
      this.setCards();
      this.isStarted = true;
    },
    getImg: function () {
      this.images = [];
      let shuffledImgs = _.shuffle(imgs);
      for (let i = 0; i < this.deckSize; i++) {
        this.images.push(shuffledImgs[i]);
      }
    },
    setCards: function () {
      let cards = [].concat(_.cloneDeep(this.images), _.cloneDeep(this.images));
      this.cards = _.shuffle(cards);
      this.loading = false;
    },
    cardOpen: function (card) {
      if (this.openCards.length === 2) {
        return
      }
      this.openCards.push(card);
      card.isFlipped = true;

      if (this.openCards.length === 2) {
        this.currentStep++;
        setTimeout(() => {
          this.handlePossibleMatch();
        }, 500)
      }
    },
    handlePossibleMatch: function () {
      if (this.cardMatch()) {
        this.matchedCards.push(this.openCards[0], this.openCards[1]);
        _.map(this.openCards, card => card.matched = true);
        this.isFinished();
      } else {
        this.closeCards();
      }
      this.openCards = [];
    },
    cardMatch: function () {
      return this.openCards[0].name === this.openCards[1].name;
    },
    closeCards: function () {
      _.map(this.openCards, card => card.isFlipped = false);
    },
    restartGame: function () {
      this.currentStep = 0;
      this.openCards = [];
      this.matchedCards = [];
      this.images = _.shuffle(this.images);
      this.setCards();
    },
    isFinished: function () {
      if (this.matchedCards.length / 2 !== this.deckSize) {
        return false;
      }
      this.bestGame = this.bestGame === 0 || this.bestGame > this.currentStep ? this.currentStep : this.bestGame;
    }
  }
}
</script>

<style scoped>

</style>