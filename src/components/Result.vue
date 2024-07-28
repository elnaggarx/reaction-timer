<template>
  <div class="result" v-if="this.finished">
    <p>{{ this.score }}ms</p>
    <p>Try harder next time</p>
    <button @click="retryClicked">Retry</button>
  </div>
</template>

<script>
export default {
  name: 'Result-comp',
  props: ['score', 'finished'],
  methods: {
    retryClicked() {
      this.$emit('retry')
    }
  }
}
</script>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
p {
  text-align: center;
  font-size: 1.2rem;
  margin-top: -13px;
}
</style>
