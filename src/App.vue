<template>
  <div id="app">
    <HelloBershka />
  </div>
</template>

<script>
import HelloBershka from './components/HelloBershka.vue'

export default {
  name: 'App',
  components: {
    HelloBershka
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
</style>
