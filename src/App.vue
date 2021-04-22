<template>
  <div id="app">
    <ChipsInput />
  </div>
</template>

<script>
import ChipsInput from './components/ChipsInput.vue'

export default {
  name: 'App',
  components: {
    ChipsInput
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
