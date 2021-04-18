<template>
  <div id="app">
    <WeatherTable></WeatherTable>
  </div>
</template>

<script>
import WeatherTable from './components/WeatherTable.vue'

export default {
  name: 'App',
  components: {
    WeatherTable
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
