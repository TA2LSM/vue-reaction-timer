<template>
    <div class="block" v-if="showBlock" @click="stopTimer">
        <p>Click Me!</p>
    </div>
</template>

<script>

  export default {
    name: 'Block',
    props: ['delay'],

    data() {
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0 
        }
    },
    
    // Lifecycle hooks
    mounted() {
        setTimeout(() => {
            this.showBlock = true;
            this.startTimer();
        }, this.delay);
    },
    // User functions
    methods: {
        startTimer() {
            this.timer = setInterval(() => {
                this.reactionTime += 10;  
            }, 10); // 10ms resolution 
        }, 
        stopTimer() {
            clearInterval(this.timer);
            this.$emit('result', this.reactionTime);
        }
    }
  }
</script>

<style>
    .block {
        width: 400px;
        border-radius: 20px;
        background: #0faf87;
        color: white;
        text-align: center;
        padding: 100px 0;
        margin: 40px auto;
    }

    .block p {
        font-size: 2rem;
        font-weight: bold;
    }
</style>