<script>
import Block from './components/Block.vue'
import Result from './components/Result.vue'

export default {
  name: 'App',
  components: { Block, Result },
  data() {
    return {
      isPlaying: false,
      delay: null,
      finished: false,
      score: 0,
      retryClicked: false
    }
  },
  methods: {
    start() {
      this.isPlaying = true
      this.delay = 2000 + 5000 * Math.random()
    },
    showResult(time) {
      this.finished = true
      this.score = time
    },
    retry() {
      this.isPlaying = false
      this.delay = null
      this.finished = false
      this.score = 0
      this.retryClicked = true
    },
    disableRetry() {
      this.retryClicked = false
    }
  }
}
</script>

<template>
  <h1>Reaction Timer Game</h1>
  <button @click="start" :disabled="isPlaying">Start</button>
  <Block
    :delay="delay"
    v-if="isPlaying"
    @end="showResult"
    :retryClicked="retryClicked"
    @disableRetryClicked="disableRetry"
  ></Block>
  <Result :score="score" :finished="finished" @retry="retry"></Result>
</template>

<style>
h1 {
  font-size: 3rem;
  color: #424242;
}
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}
#app button {
  border-radius: 12px;
  padding: 10px 30px;
  border: solid 1px #0faf87;
}
#app button:hover {
  cursor: pointer;
}
</style>
