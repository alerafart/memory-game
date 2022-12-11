<template>
  <p @click="start">Timer {{time}} {{currentTime}}</p>
</template>

<script>
import constants from '../assets/constants';
export default {
    
  // eslint-disable-next-line vue/multi-word-component-names
  name: "xTimer",
  data() {
    return {
      time: "00:00",
      currentTime:'0',
      timeBegan: null,
      timeStopped: null,
      stoppedDuration: 0,
      started: null,
      running: false,
    };
  },
  watch: {
    startStatus(newValue) {
      if (newValue === constants.TIMER_START) this.start()
      else if (newValue === constants.TIMER_STOP) this.stop()
      else this.reset()
    }
  },
  methods: {
    start() {
      if (this.running) return;
      if (this.timeBegan === null) {
        this.reset();
        this.timeBegan = new Date();
      }
      if (this.timeStopped !== null) this.stoppedDuration += new Date() - this.timeStopped;
      this.started = setInterval(this.clockRunning, 10);
      this.running = true;
    },
    stop() {
      this.running = false;
      this.timeStopped = new Date();
      clearInterval(this.started);
    },
    reset() {
      this.running = false;
      clearInterval(this.started);
      this.stoppedDuration = 0;
      this.timeBegan = null;
      this.timeStopped = null;
      this.time = "00:00";
    },
    clockRunning() {
      var currentTime = new Date(),
        timeElapsed = new Date(currentTime - this.timeBegan - this.stoppedDuration),
        // hour = timeElapsed.getUTCHours(),
        min = timeElapsed.getUTCMinutes(),
        sec = timeElapsed.getUTCSeconds()
        // ms = timeElapsed.getUTCMilliseconds();
        // this.zeroPrefix(hour, 2)
        // this.zeroPrefix(ms, 3);
      this.time = `${this.zeroPrefix(min, 2)}:${this.zeroPrefix(sec, 2)}`
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
