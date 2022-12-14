<template>
  <p class="timer">Timer {{ time }}</p>
</template>

<script>
// import {ref} from 'vue';
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Timer",
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
  props: ['flipy'],
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
  // watch prop flipy comming from 'flip:null' in parents data
  // on first click on a card it changes and this will trigger timer to start
  watch: { 
      flipy: function(newVal, oldVal) { // watch it
          console.log('Prop changed: ', newVal, ' | was: ', oldVal)
          this.start()
        }
      }

};
</script>

<style>
.timer {
  border-radius: 5px;
  border: 1px solid gray;
  width: 20rem;
  padding: 2px;
  font-size: 1.5rem;
  font-weight: bold;
  color:rgb(99, 98, 98);
}
</style>
