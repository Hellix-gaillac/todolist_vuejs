<template>
  <div class="counter">
    {{ count }}
    <div class="counter__button asc" @click="increment()">Incrementer</div>
    <div class="counter__button desc" @click="decrement()">Décrementer</div>
  </div>
</template>

<script>
import store from "../store/NotificationsStore";

export default {
  data() {
    return {
      state: store.state
    };
  },
  computed: {
    count() {
      return this.state.count;
    }
  },
  methods: {
    increment() {
      store.increment()
    },
    decrement() {
      store.decrement()
    }
  }
};
</script>

<style ="sass">
.counter{
    background-color: blue;
}
.counter__button {
  width: 100px;
  color: aliceblue;
}
.asc {
  margin: 10px;
  background-color: #279f87;
}
.desc {
  margin: 10px;
  background-color: red;
}
</style>

