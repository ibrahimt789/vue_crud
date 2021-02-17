<template>
  <button class="p-5 bg-blue-500 border-2  rounded-3xl m-5 b"  @click="invokeParent">Toggle Counter</button>
  <h1>Hello {{ name }}!!</h1>
  <template v-if="showCounter">
    <input v-model="name" />
    <br />
    <button @click="incCounter">+</button>
    <p>{{ counter }}</p>
    <button @click="decCounter">-</button>
  </template>
</template>

<script>
export default {
  name: "CounterApp",
  props: ["title", "initialCounterValue", "toggleCounterView"],
  data() {
    return {
      name: "Khaleelullah",
      counter: this.initialCounterValue
        ? parseInt(this.initialCounterValue)
        : 0,
      showCounter: false,
    };
  },
  methods: {
    incCounter() {
      this.counter += 1;
    },
    decCounter() {
      if (this.counter > 0) {
        this.counter -= 1;
      } else {
        alert("can't decrement to minus");
      }
    },
    invokeParent() {
      this.showCounter = !this.showCounter;
      this.$emit("toggleCounter", this.showCounter);
    },
  },
};
</script>
