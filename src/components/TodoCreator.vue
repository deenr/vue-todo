<template>
  <div class="flex items-center border-b border-teal-500 py-2">
    <input
      class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
      type="text"
      v-model="todoState.todo"
    />
    <TodoButton @click="createTodo()" />
  </div>
  <p class="err-msg" v-if="todoState.invalid">{{ todoState.errMsg }}</p>
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
