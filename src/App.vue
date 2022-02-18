<template>
  <div id="app">
    
    <chart/>
  </div>
</template>

<script>
import chart from './components/Chart.vue'

export default {
  name: 'App',
  components: {
    chart
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
  max-width: 800px;
  max-height: 500px;
}
</style>
