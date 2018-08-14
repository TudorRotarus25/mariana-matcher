<template>
  <div id="app">
    <Matcher/>
  </div>
</template>

<script>
import Matcher from './components/Matcher.vue'

export default {
  name: 'app',
  components: {
    Matcher
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
