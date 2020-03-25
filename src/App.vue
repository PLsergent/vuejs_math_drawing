<template>
  <div id="app">
    <h1>Math function drawing</h1>
    <VueCanvas />
  </div>
</template>

<script>
import VueCanvas from "./components/Canvas.vue";


export default {
  name: "App",
  components: {
    VueCanvas
  }
};
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
