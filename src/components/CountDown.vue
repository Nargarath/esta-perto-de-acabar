<template>
  <div id="countDown">
    <p id="message">{{ closeToOver ? 'Sim' : 'Não' }}</p>
    <p id="timer">{{ time }}</p>
    
  </div>
</template>

<script>
export default {
  name: 'CountDown',
  props: {
    totalMinutes: {
      type: Number,
      default: 0
    },
    timing: {
      type: Boolean,
      default: false
    },
  },
  data() {
    return {
      localTimeSeconds: 0
    }
  },
  watch: {
    timing:{
      handler: function(newValue,oldValue) {
        if (!oldValue && newValue) {
          this.startLocalTime();
        }
      },
      deep: true
    } 
  },
  computed: {
    closeToOver() {
      return this.localTimeMinutes < 30;
    },
    time() {
      const time = this.localTimeSeconds;
      const minutes = Math.floor(time / 60);
      const seconds = time - (minutes * 60);
      return `${minutes}:${seconds}`;
    },
  },
  methods: {
    startLocalTime() {
      this.localTimeSeconds = this.totalMinutes * 60;
    },
    startTimeCounter() {
      setInterval(
        () => { 
          if (this.timing && (this.localTimeSeconds / 60) <= this.totalMinutes ) {
            this.localTimeSeconds--;
          }
        }, 
      1000);
    }
  },
  mounted() {
    this.startLocalTime();
    this.startTimeCounter();
  }
}
</script>

<style scoped>
  #timer {
    font-size: 47px;
    color: white;
    font-weight: bold;
    margin-top: 10px;
    margin-bottom: 10px;
  }
  #message {
    color: red;
    font-weight: bold;
    font-size: 60px;
    margin: 0;
  }
</style>
