<template>
  <div id="app">
    <carousel>
      <carousel-slide>
        SALUT
        <img src="https://picsum.photos/id/215/200/300" alt>
      </carousel-slide>
      <carousel-slide>
        AUREVOIR
        <img src="https://picsum.photos/id/200/200/300" alt>
      </carousel-slide>
      <carousel-slide>
        AUREVOIR
        <img src="https://picsum.photos/id/210/200/300" alt>
      </carousel-slide>
      <carousel-slide>
        AUREVOIR
        <img src="https://picsum.photos/id/120/200/300" alt>
      </carousel-slide>
      <carousel-slide>
        AUREVOIR
        <img src="https://picsum.photos/id/320/200/300" alt>
      </carousel-slide>
    </carousel>

    <img src="./assets/logo.png">
    {{todosApp}}
    <button @click="addTodos">Ajouter todos</button>
    <h2>TODO1</h2>
    <todos v-model="todosApp"></todos>
    <h2>TODO1bis</h2>
    <todos v-model="todosApp"></todos>
  </div>
</template>

<script>
import Carousel from "./components/carousel/Carousel.vue";
import CarouselSlide from "./components/carousel/CarouselSlide.vue";

import Todos from "./components/Todos.vue";
import TodosVue from "./components/Todos.vue";

export default {
  name: "App",
  components: {
    Todos,
    Carousel,
    CarouselSlide
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
