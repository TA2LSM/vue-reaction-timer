<template>
  <h1>{{ title }}</h1>
  <br>

  <button @click="startGame" :disabled="isPlaying ">Play Game</button>
  <Block v-if="isPlaying" :delay="delay" @result="endGame"/>
  <Results v-if="isGameEnded" :gameScore="gameScore" />   
</template>


<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'


export default {
  name: 'App',   
  components: {
    Block,
    Results
  },

  data() {
    return {
      title: "~ Vue Reaction Timer  ~",
      isPlaying: false, 
      isGameEnded: false,
      delay: null, 
      gameScore: 0
    }
  },

  methods: {
    startGame() {
      this.isPlaying = true;
      this.isGameEnded = false; 
      this.delay = 2000 + (Math.random() * 5000);
    },
    endGame(finalReactionTime) {
        this.gameScore = finalReactionTime;
        this.isGameEnded = true;
        this.isPlaying = false;
    }
  },
}
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

  h1 {
    border-bottom: 1px solid #ddd;
    display: inline-block;
    padding-bottom: 10px;
  }

  button {
    width: 15 0px;
    background-color: #0faf87;
    color: white;
    border: none;
    padding: 8px, 16px;
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
</style>
