<template>
  <section class="todo-list">
    <h3>TODO LIST</h3>
    <div class="list">
      <div
        v-for="todo in todos"
        :class="`todo-item ${todo.done && 'done'}`"
        :key="todo.content"
      >
        <label>
          <!-- <input type="checkbox" v-model="todo.done" /> -->
          <input
            type="checkbox"
            :value="todo.done"
            @input="checkboxHandler(todo, $event)"
          />
        </label>

        <span class="todo-content">
          <input type="text" :value="todo.content" @input="contentHandler(todo, $event)" />
        </span>
        <span>
          <button class="delete" @click="$emit('removeTodo', todo)">
            DELETE
          </button>
        </span>
      </div>
    </div>
  </section>
</template>

<script lang="ts" setup>
import { toRefs, defineProps, defineEmits, Ref } from "vue";
import TodoItem from "../type";

const props: { todos: Ref<TodoItem>; removeTodo: Function } = defineProps([
  "todos",
  "removeTodo",
]);
const emit = defineEmits(["removeTodo"]);

const checkboxHandler = (todo: TodoItem, event: Event) => {
  todo.done = !todo.done;
};

const contentHandler = (todo: TodoItem, event: Event) => {
  todo.content = event.target.value;
};
</script>

<style></style>
