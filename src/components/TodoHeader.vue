<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <header>
    <nav class="flex justify-between py-4 px-4">
      <div class="flex center-align">
        <img class="w-8 h-8" src="../assets/dr.svg" alt="Vue logo" />
        <h1 class="text-teal-500 flex items-center font-bold pl-2">
          Vue Todos
        </h1>
      </div>
      <ul class="flex items-center center-align text-teal-500">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink class="pl-4" to="/about">About</RouterLink>
      </ul>
    </nav>
  </header>
</template>

<style lang="scss" scoped></style>
