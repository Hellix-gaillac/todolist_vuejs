<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todo</h1>
      <input
        type="text"
        class="new-todo"
        placeholder="Ajouter une tâche"
        v-model="newTodo"
        @keyup.enter="addTodo()"
      >
    </header>
    <section class="main">
      <input type="checkbox" class="toggle-all" v-model="allDone">
      <label for="toggle-all"></label>
      <ul class="todo-list">
        <li
          class="todo"
          v-for="todo in filteredTodos"
          :class="{completed: todo.completed, editing: todo===editing}"
          :key="todo.name"
        >
          <div class="view">
            <input type="checkbox" v-model="todo.completed" class="toggle">
            <label @dblclick="editTodo(todo)">{{todo.name}}</label>
            <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
          </div>
          <input
            type="text"
            class="edit"
            v-model="todo.name"
            @keyup.enter="doneEdit"
            @keyup.escape="cancelEdit"
            v-focus="todo===editing"
            @blur="doneEdit"
          >
        </li>
      </ul>
      <button class="clear-completed" @click.prevent="deleteCompleted" v-show="completed">
        supprimer
        <br>tâches
        completées
      </button>
    </section>
    <footer class="footer" v-show="todos.length >0">
      <span class="todo-count">
        <strong>{{remaining}}</strong> tâche(s) à faire
      </span>
      <ul class="filters">
        <li>
          <a href="#" :class="{selected:filter === 'all'}" @click.prevent="filter = 'all'">TOUTES</a>
        </li>
        <li>
          <a href="#" :class="{selected:filter === 'todo'}" @click.prevent="filter = 'todo'">à faire</a>
        </li>
        <li>
          <a
            href="#"
            :class="{selected:filter === 'done'}"
            @click.prevent="filter = 'done'"
          >faite(s)</a>
        </li>
      </ul>
    </footer>
  </section>
</template>


<script>
import Vue from "vue";
export default {
  props: {
    value: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  data() {
    return {
      todos: this.value,
      newTodo: "",
      filter: "all",
      editing: null,
      oldTodo: ""
    };
  },
  watch: {
    value(value) {
      this.todos = value;
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo !== "") {
        this.todos.push({
          completed: false,
          name: this.newTodo
        });
      }
      this.newTodo = "";
    },
    deleteTodo(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1);
      this.$emit("input", this.todos);
    },
    deleteCompleted() {
      this.todos.forEach(todo => {
        if (todo.completed) {
          this.todos.splice(this.todos.indexOf(todo));
        }
        this.$emit("input", this.todos);
      });
      //this.todos = this.todos.filter(todo =>!todo.completed)
    },
    editTodo(todo) {
      this.editing = todo;
      this.oldTodo = todo.name;
    },
    doneEdit() {
      this.editing = null;
    },
    cancelEdit() {
      this.editing.name = this.oldTodo;
      this.doneEdit();
    }
  },
  computed: {
    completed() {
      return this.todos.filter(todo => todo.completed).length;
    },
    remaining() {
      return this.todos.filter(todo => !todo.completed).length;
    },
    filteredTodos() {
      if (this.filter === "todo") {
        return this.todos.filter(todo => !todo.completed);
      } else if (this.filter === "done") {
        return this.todos.filter(todo => todo.completed);
      } else {
        return this.todos;
      }
    },
    allDone: {
      get() {
        return this.remaining === 0;
      },
      set(value) {
        this.todos.forEach(todo => (todo.completed = value));
      }
    }
  },
  directives: {
    focus(el, value) {
      Vue.nextTick().then(function() {
        if (value) {
          el.focus();
        }
      });
    }
  }
};
</script>





<style src="..\assets\css\todo.css"></style>
