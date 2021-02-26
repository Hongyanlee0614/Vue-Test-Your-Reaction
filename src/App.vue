<template>
  <h1>Test Your Reaction</h1>
  <button @click="start" :disabled="isPlaying">PLAY</button>
  <br />
  <!-- Results -->
  <Results v-if="showResults" :score="score" />
  <p class="fault">{{ faultScore }}</p>
  <!-- Instructions -->
  <br />
  <p v-if="!isPlaying">How to play?</p>
  <br />
  <p v-if="!isPlaying">1. Click the PLAY button.</p>
  <p v-if="!isPlaying">
    2. Wait for a green box to appear within a few seconds. Do not click before
    the box appear!
  </p>
  <p v-if="!isPlaying">3. Left click the box as soon as you see it.</p>
  <p v-if="!isPlaying">4. View your reaction level!</p>

  <!-- Block -->
  <!-- pass in the delay property as prop so that block component can be shown accordingly -->

  <Block
    v-if="isPlaying"
    :delay="delay"
    @end="endGame"
    @endFault="endGameFault"
  />
</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";
export default {
  name: "App",
  components: { Block, Results },
  data() {
    return {
      //keep track of whether is now playing or not, false to begin with
      isPlaying: false,
      //amount of time before the block appears after user clicks PLAY
      delay: null,
      //final reaction time of user
      score: null,
      showResults: false,
      faultScore: "",
    };
  },
  methods: {
    start() {
      this.faultScore = "";
      //the block will appear between 2-7s
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResults = false;
    },
    endGame(reactionTime) {
      this.score = reactionTime;
      this.isPlaying = false;
      this.showResults = true;
    },
    endGameFault() {
      this.isPlaying = false;
      this.faultScore = "Too Fast";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
.fault {
  font-size: 1rem;
  color: red;
  font-weight: bold;
}
</style>
