<template>
  <p @click="start">Timer {{ time }}</p>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Timer2",
  data() {
    return {
      time: "00:00",
      currentTime: "0",
      timeBegan: null,
      timeStopped: null,
      stoppedDuration: 0,
      started: null,
      running: false,
    };
  },

  methods: {
    start() {
      this.currentTime = new Date();
      if (this.running) return;

      if (this.timeBegan === null) {
        this.timeBegan = new Date();
      }
      if (this.timeStopped !== null) {
        this.stoppedDuration += new Date() - this.timeStopped;
      }
      this.started = setInterval(this.clockRunning, 10);
      this.running = true;
    },

    clockRunning() {
      let currentTime = new Date(),
        timeElapsed = new Date(
          currentTime - this.timeBegan - this.stoppedDuration
        ),
        min = timeElapsed.getUTCMinutes(),
        sec = timeElapsed.getUTCSeconds();
      this.time = this.zeroPrefix(min, 2) + ":" + this.zeroPrefix(sec, 2);
    },
    stop() {
      this.running = false;
      this.timeStopped = new Date();
      clearInterval(this.started);
    },
    zeroPrefix(num, digit) {
      var zero = "";
      for (var i = 0; i < digit; i++) {
        zero += "0";
      }
      return (zero + num).slice(-digit);
    },
  },
};
</script>

<style></style>
