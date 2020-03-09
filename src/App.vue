<template>
  <div id="app">
    <h1>WHCC Hacker News Reader</h1>
    <stories></stories>
  </div>
</template>

<script>
import Stories from './components/Stories.vue'

export default {
  name: 'App',
  components: {
    Stories
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  text-align: center;
  color: forestgreen;
}
</style>
