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
          <button class="button delete" @click="$emit('removeTodo', todo)">
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

const props: { todos: TodoItem[] } = defineProps([
  "todos"
]);

const emit = defineEmits(["removeTodo"]);

const checkboxHandler = (todo: TodoItem, event: InputEvent) => {
  const updatedTodo = { ...todo };
  updatedTodo.done = !updatedTodo.done;
  
  // index 업데이트
  const index = props.todos.indexOf(todo);
  if (index !== -1) {
    props.todos[index] = updatedTodo;
  }
};

const contentHandler = (todo: TodoItem, event: InputEvent) => {
  const updatedTodo = { ...todo };
  updatedTodo.content = event.target.value;

  // index 업데이트
  const index = props.todos.indexOf(todo);
  if (index !== -1) {
    props.todos[index] = updatedTodo;
  }
};
</script>

<style></style>
