<template>
  <section class="greeting">
    <h2 class="title">
      Hello, <input type="text" placeholder="name" v-model="name" id="name" />
    </h2>
  </section>

  <section class="create-todo">
    <h3>Create a todo.</h3>
    <form @submit.prevent="addTodo">
      <input type="text" placeholder="write" v-model="inputContent" />
      <button type="submit" class="button">ADD</button>
    </form>
  </section>
  <!-- <TodoInput :inputContent="inputContent" @addTodo="addTodo" /> -->

  <TodoList :todos="todos" @removeTodo="removeTodo" />
</template>

<script lang="ts" setup>
import { ref, onMounted, computed, watch } from "vue";
import TodoList from "./components/TodoList.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoItem from "./type";

const todos = ref<TodoItem[]>([]);
const name = ref<string>("");
const inputContent = ref<string>("");

onMounted(() => {
  name.value = localStorage.getItem("name") || "";
  todos.value = JSON.parse(localStorage.getItem("todos")) || [];
});

const addTodo = () => {
  if (inputContent.value.trim() === "") {
    return;
  }

  todos.value.push({
    content: inputContent.value,
    done: false,
  });

  inputContent.value = "";
};

const removeTodo = (todo: TodoItem) => {
  todos.value = todos.value.filter((t) => t !== todo);
};

watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  { deep: true }
);

watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});
</script>

<style class="scss">
#app {
  padding: 40px;
  text-align: center;
  color: #2c3e50;
  background-color: lightgray;
}
</style>
