<template>
  <p>Initialise counter with 5</p>

  <CounterApp
    title="hello from props"
    :initialCounterValue="0"
    @toggleCounter="toggleCounterView"
  />
  <Users />
  <ul>
    <li :key="index" v-for="(todo, index) of todos">
      {{ todo }}
      <button
        @click="deleteTodo(todo, index)"
        class="bg-red-600 active:bg-red-400"
      >
        Delete
      </button>
    </li>
  </ul>

  <input placeholder="Enter New Task to Add" @input="storeTodo($event)" />
  <button @click="addTodo()">Add</button>
</template>
<script>
import CounterApp from "./CounterApp.vue";
import Users from "./RandomUsers.vue";
export default {
  components: { CounterApp, Users },
  data() {
    return {
      currentTodos: "",
      todos: ["Wake up", "pray", "Recite", "exercise"],
      showCounter: false,
    };
  },
  methods: {
    storeTodo(eve) {
      this.currentTodos = eve.target.value;
    },
    toggleCounterView(params) {
      this.showCounter = params;
    },
    addTodo() {
      const isDuplicateTodo = this.todos.find((td) => td === this.currentTodos);
      if (isDuplicateTodo) {
        alert("Same Todo already Exist!");
      } else {
        this.todos = this.todos.concat(this.currentTodos);
      }
    },
    deleteTodo(deletedTodo) {
      this.todos = this.todos.filter((t) => t !== deletedTodo);
    },
  },
};
</script>
