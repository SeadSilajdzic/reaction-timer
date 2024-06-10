<template>
    <h1>Reaction timer</h1>
    <button @click="start" :disabled="isPlaying">Play</button>
    <Block v-if="isPlaying" :delay="delay" @reactionTime="endGame"/>
    <Results v-if="showResults" :score="score"/>
</template>

<script>
import Block from './components/Block.vue'
import Results from "@/components/Results.vue";

export default {
    name: 'App',
    components: {Results, Block},
    data() {
        return {
            isPlaying: false,
            delay: null,
            score: null,
            showResults: false,
        }
    },
    methods: {
        start() {
            this.delay = 2000 + Math.random() * 5000;
            this.isPlaying = true;
            this.showResults = false;
        },

        endGame(reactionTime) {
            this.isPlaying = false;
            this.score = reactionTime;
            this.showResults = true;
        }
    }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #444;
    margin: 60px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

button {
    background: #0faf87;
    color: white;
    border: none;
    border-radius: 4px;
    padding: 8px 16px;
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
