<script setup>
import { Icon } from "@iconify/vue";

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
  index: {
    type: Number,
    required: true,
  },
});

defineEmits([
  "toggle-complete",
  "toggle-editing",
  "update-todo",
  "delete-todo'",
]);
</script>

<template>
  <li class="flex justify-between py-1">
    <div>
      <input
        class="accent-pink-500"
        type="checkbox"
        :checked="todo.isCompleted"
        @input="$emit('toggle-complete', index)"
      />
      <input
        v-if="todo.isEditing"
        class="mx-2"
        type="text"
        :value="todo.todo"
        @input="$emit('update-todo', $event.target.value, index)"
      />
      <span
        class="mx-2"
        :class="{
          'line-through': todo.isCompleted,
        }"
        v-else
        >{{ todo.todo }}</span
      >
    </div>
    <div class="flex flex-row items-center">
      <Icon
        v-if="todo.isEditing"
        icon="mdi:checkbox-marked-circle-outline"
        @click="$emit('toggle-editing', index)"
      />
      <Icon
        v-else
        icon="mdi:pencil-outline"
        @click="$emit('toggle-editing', index)"
      />
      <Icon icon="mdi:delete-outline" @click="$emit('delete-todo', todo.id)" />
    </div>
  </li>
</template>

<style lang="scss" scoped></style>
