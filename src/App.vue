<template>
  <div id="app">
    <wedding />
  </div>
</template>

<script>
import Wedding from './components/Wedding'

export default {
  name: "app",
  components: {
    wedding: Wedding
  }
};
</script>

<style>
body {
  background-color: #f4f4f4;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
