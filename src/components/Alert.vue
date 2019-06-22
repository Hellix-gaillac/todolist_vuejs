<template>
  <div>
    <transition name="bounce" appear mode="out-in">
      <div class="message success" v-if="visible" key="visible">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Consequatur,
        maiores commodi non ipsum, libero voluptates in enim vel accusamus minus nostrum dolores? Ab, incidunt omnis ut
        veritatis quae accusantium nobis!
      </div>
      <div class="message success" v-else key="invisible">Je suis un test</div>
    </transition>
    <button @click="toggle">Button</button>

    <transition-group name="fade" tag="ul">
      <li v-for="item in items" :key="item">{{item}}</li>
    </transition-group>

    <button @click="add">Ajouter</button>
    <button @click="shuffle">shuffle</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      visible: true,
      items: [1, 2, 3, 4, 5]
    };
  },
  methods: {
    toggle() {
      this.visible = !this.visible;
    },
    add() {
      this.items.push(Math.random());
    },
    shuffle() {
      this.items = [2, 3, 5, 4, 6];
    }
  }
};
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s, transform 0.8s;
}
.fade-enter,
.fade-leave-active {
  opacity: 0;
  transform: translateX(80px);
}
.fade-move {
  transition: transform 5s;
}
.bounce-enter-active {
  animation: bounce-in 1s;
}
.bounce-leave-active {
  animation: bounce-in 1s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
</style>
