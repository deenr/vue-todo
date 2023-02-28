<script setup>
import { RouterView } from "vue-router";
import TodoHeader from "./components/TodoHeader.vue";
</script>

<template>
  <TodoHeader />
  <RouterView />
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Rubik:wght@300;400;500;700&display=swap");

* {
  font-family: "Rubik", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-size: cover;
  background-repeat: no-repeat;
  background-position-y: -10vw;
  background-position-x: 100%;
  background-image: url("./assets/background-green.svg");
}
</style>
