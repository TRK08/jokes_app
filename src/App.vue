<template>
  <div id="app">
    <Jokes />
  </div>
</template>

<script>
import "./assets/css/style.css";
import Jokes from "./pages/Jokes.vue";

export default {
  components: { Jokes },
  name: "App",
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
