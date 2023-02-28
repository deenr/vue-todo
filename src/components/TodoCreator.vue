<template>
  <div class="flex items-center border-b border-white py-2">
    <input
      class="appearance-none bg-transparent border-none w-full text-white placeholder-white/50 mr-3 py-1 px-2 leading-tight focus:outline-none"
      type="text"
      placeholder="Create your new task here"
      v-model="todoState.todo"
    />
    <TodoButton @click="createTodo()" />
  </div>
  <p class="text-teal-500 text-sm" v-if="todoState.invalid">
    {{ todoState.errMsg }}
  </p>
</template>

<script setup>
import { reactive } from "vue";
import TodoButton from "./TodoButton.vue";
const todoState = reactive({
  todo: "",
  invalid: null,
  errMsg: "",
});

const emit = defineEmits(["create-todo"]);

const createTodo = () => {
  todoState.invalid = null;

  if (todoState.todo !== "") {
    emit("create-todo", todoState.todo);
    todoState.todo = "";
    return;
  }

  todoState.invalid = true;
  todoState.errMsg = "Todo value can not be empty";
};
</script>

<style lang="scss" scoped></style>
