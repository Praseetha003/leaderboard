<template>
  <div id="app">
    <LeaderBoard/>
  </div>
</template>

<script>
import LeaderBoard from './components/LeaderBoard.vue'

export default {
  name: 'App',
  components: {
    LeaderBoard
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
