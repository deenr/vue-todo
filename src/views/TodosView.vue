<script setup>
import { Icon } from "@iconify/vue";
import { ref, watch, computed } from "vue";
import { uid } from "uid";
import TodoCreator from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";

const todoList = ref([]);

watch(
  todoList,
  () => {
    setTodoListLocalStorage();
  },
  { deep: true }
);

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
  if (savedTodoList) {
    todoList.value = savedTodoList;
  }
};

fetchTodoList();

const setTodoListLocalStorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: false,
    isEditing: false,
  });
};

const toggleTodoComplete = (todoIndex) => {
  todoList.value[todoIndex].isCompleted =
    !todoList.value[todoIndex].isCompleted;
};

const toggleTodoEditing = (todoIndex) => {
  todoList.value[todoIndex].isEditing = !todoList.value[todoIndex].isEditing;
};

const updateTodo = (todoValue, todoIndex) => {
  todoList.value[todoIndex].todo = todoValue;
};

const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
};

const todosCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted === true);
});
</script>

<template>
  <main class="flex items-center justify-center">
    <div class="w-96">
      <h1
        class="font-bold text-2xl text-center object-contain text-white pt-[10vw] pb-4"
      >
        Create todo
      </h1>
      <TodoCreator @create-todo="createTodo"></TodoCreator>
      <ul v-if="todoList.length > 0" class="mt-2">
        <TodoItem
          class="border-dashed border-b-2 border-white"
          v-for="(todo, index) in todoList"
          :todo="todo"
          :index="index"
          @toggle-complete="toggleTodoComplete"
          @toggle-editing="toggleTodoEditing"
          @update-todo="updateTodo"
          @delete-todo="deleteTodo"
        />
      </ul>
      <p v-else class="no-todos-msg">
        <Icon icon="mdi:emoticon-sad-outline" />
        <span>You have no todo's to complete.</span>
      </p>
      <p
        v-if="todosCompleted && todoList.length > 0"
        class="flex items-center justify-center mt-4"
      >
        <Icon class="text-white text-5xl" icon="mdi:party-popper" />
        <span class="text-white pl-2">All todo's are completed.</span>
      </p>
    </div>
  </main>
</template>

<style lang="scss" scoped></style>
