<template>
  <div
    class="block"
    v-if="show"
    @click="
      () => {
        finished = !finished
      }
    "
  >
    Click me
  </div>
</template>

<script>
export default {
  name: 'Block-comp',
  props: ['delay', 'retryClicked'],
  data() {
    return {
      show: false,
      time: 0,
      finished: false
    }
  },
  methods: {
    checkTime() {
      setTimeout(() => {
        this.show = true
        this.Timer()
      }, this.delay)
    },
    Timer() {
      setInterval(() => {
        if (this.finished === true) {
          this.$emit('end', this.time)
          clearInterval()
        } else {
          this.time += 10
        }
      }, 10)
    }
  },
  mounted() {
    this.checkTime()
  },
  unmounted() {
    if (this.retryClicked === true) {
      ;(this.show = false), (this.time = 0), (this.finished = false)
      this.$emit('disableRetryClicked')
    }
  }
}
</script>

<style scoped>
.block {
  background-color: #0faf87;
  padding: 100px 0;
  border-radius: 20px;
  width: 400px;
  text-align: center;
  margin: 40px 0;
}
.block:hover {
  cursor: pointer;
}
</style>
