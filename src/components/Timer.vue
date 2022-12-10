<template>
  <p>Timer {{time}}</p>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Timer",
  data() {
    return {
      time: "00:00",
      timeBegan: null,
      timeStopped: null,
      stoppedDuration: 0,
      started: null,
      running: false,
    };
  },
};
</script>

<style></style>
