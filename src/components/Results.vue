<template>
  <div class="results">
    <p>Reaction Time: {{ gameScore }}ms</p>
    <p class="rank">{{ rank }}</p>
  </div>
</template>

<script>
  export default {
    name: 'Results',
    props: {
      gameScore: Number,
    },
    
    data() {
      return {
        rank: null,
      }
    },

    mounted() {
      if(this.gameScore < 250)  {
        this.rank = 'Magnificent Reflexes';
      } else if (this.gameScore < 450) {
        this.rank = 'Rapid Reflexes';
      } else {
        this.rank = 'Snail pace...';
      }
    }
  }
</script>

<style>
  .rank {
    font-size: 1.4rem;
    color: #0faf87;
    font-weight: bold;
  }

  .results p {
    font-size: 1.2rem;
    font-weight: bold;
  }
</style>
