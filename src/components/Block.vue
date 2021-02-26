<template>
  <div class="block" v-if="showBlock" @click="stopTimer">Click Me</div>
  <div class="block2" @click="fault" v-else>Do not click me first</div>
</template>

<script>
export default {
  props: ["delay"],
  data() {
    return {
      //don't want to show the block as soon as user clicks PLAY
      showBlock: false,
      //store the elapsed time interval after block appears
      timer: null,
      reactionTime: 0,
    };
  },
  //once the block is mounted to the DOM
  mounted() {
    //after that amount of delay only show the block
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },
  methods: {
    //start at soon as the block appears
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer);
      this.$emit("end", this.reactionTime);
    },
    stopTimerFault() {
      clearInterval(this.timer);
      this.$emit("endFault");
    },
    fault() {
      this.stopTimerFault();
    },
  },
};
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
.block2 {
  width: 400px;
  border-radius: 20px;
  background: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
  opacity: 0;
}
</style>
