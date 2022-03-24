<template>
  <div id="app">
    <MoneyConverter />
  </div>
</template>

<script>
import MoneyConverter from './components/MoneyConverter.vue'

export default {
  name: 'App',
  components: {
    MoneyConverter
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
