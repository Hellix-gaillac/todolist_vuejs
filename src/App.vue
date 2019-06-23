<template>
  <div id="app">
    <img src="./assets/logo.png">
    <todos></todos>
  </div>
</template>

<script>
import Todos from "./components/Todos.vue";

export default {
  name: "App",
  components: {
    Todos
  }
};
</script>

<style>
</style>
