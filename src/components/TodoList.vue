<template>
  <section class="todo-list">
    <h3>TODO LIST</h3>
    <div class="list">
      <!-- <div :class="`todo-item`">
        <label>
          <input
            type="checkbox"
            :value="todos[0]?.done"
            @input="checkboxHandler(todos[0], $event)"
          />
        </label>

        <span class="todo-content">
          <input
            type="text"
            :value="todos[0]?.content"
            @input="contentHandler(todos[0], $event)"
          />
        </span>
        <span>
          <button class="button delete" @click="$emit('removeTodo', todos[0])">
            DELETE
          </button>
        </span>
      </div> -->
      <div
        v-for="todo in todos"
        :class="`todo-item ${todo.done && 'done'}`"
        :key="todo.id"
      >
        <label>
          <input
            type="checkbox"
            :checked="todo.done"
            @input="checkboxHandler(todo, $event)"
          />
        </label>

        <span class="todo-content">
          <input
            type="text"
            :value="todo.content"
            @input="contentHandler(todo, $event)"
          />
        </span>
        <span>
          <button class="button delete" @click="$emit('removeTodo', todo)">
            DELETE
          </button>
        </span>
      </div>
    </div>
  </section>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits, PropType } from "vue";
import TodoItem from "@/type";

const props = defineProps({
  todos: {
    type: Array as PropType<Array<TodoItem>>,
    required: true,
  },
});

const emit = defineEmits<{
  removeTodo: [TodoItem];
  updateTodo: [TodoItem];
}>();

const checkboxHandler = (todo: TodoItem, event: Event) => {
  const updatedTodo = { ...todo };
  updatedTodo.done = (event.target as HTMLInputElement).checked;
  emit("updateTodo", updatedTodo);
};

const contentHandler = (todo: TodoItem, event: Event) => {
  const updatedTodo = { ...todo };
  updatedTodo.content = (event.target as HTMLInputElement).value;
  emit("updateTodo", updatedTodo);
};
</script>

<style></style>
