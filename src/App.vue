<template>
  <div id="app">
    <h1>Está perto de acabar?</h1>
    <input type="number" v-model="timeToCount">
    <count-down :total-minutes="timeToCount" :timing="timing"/>
    <button @click="toggleTimer()">{{ toggleTimerText }}</button>
  </div>
</template>

<script>
import CountDown from './components/CountDown'
export default {
  name: 'app',
  components: {
    CountDown
  },
  data() {
    return {
      timing: false,
      timeToCount: 0
    }
  },
  computed: {
    toggleTimerText() {
      return !this.timing ? 'Iniciar' : 'Parar'
    }
  },
  methods: {
    toggleTimer() {
      this.timing = !this.timing;
    }
  }
}
</script>
<style scoped>
  h1 {
    color: white;
    text-transform: uppercase;
  }
  input {
    margin-bottom: 1rem;
  }
</style>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  flex-direction: column;
}
body {
  height: 100vh;
  background-color: #49B587;
}
</style>
