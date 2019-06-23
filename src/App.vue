<template>
  <div id="app">
    <img src="./assets/logo.png">
    {{todosApp}}
    <button @click="addTodos">Ajouter todos</button>
    <h2>TODO1</h2>
    <todos v-model="todosApp"></todos>
    <h2>TODO1bis</h2>
    <todos v-model="todosApp"></todos>
    <h2>TODO3</h2>
    <todos></todos>
    <h2>TODO3</h2>
    <todos></todos>
  </div>
</template>

<script>
import Todos from "./components/Todos.vue";
import TodosVue from "./components/Todos.vue";

export default {
  name: "App",
  components: {
    Todos
  },
  data() {
    return {
      todosApp: [
        {
          name: "Xav",
          completed: true
        }
      ]
    };
  },
  methods: {
    addTodos() {
      this.todosApp.push({
        name: "Amande",
        completed: false
      });
    }
  }
};
</script>

<style>
</style>
