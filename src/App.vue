<template>
  <section class="greeting">
    <div class="container">
      <h2 class="title">
        Hello, <input type="text" placeholder="name" v-model="name" id="name" />
      </h2>
    </div>
  </section>

  <section class="create-todo">
    <h3>Create a todo.</h3>

    <form @submit.prevent="addTodo">
      <input type="text" placeholder="write" v-model="inputContent" />
      <!-- <input type="submit" value="Add Todo"> -->
      <button type="submit">Add</button>
    </form>
  </section>
  <TodoList :todos="todos" />
</template>

<script lang="ts" setup>
import { ref, onMounted, computed, watch } from "vue";
import TodoList from "./components/TodoList.vue";

const props = defineProps<{
  content: string
  done: boolean
  createdAt?: Date
}>()

const todos = ref([]);
const name = ref("");
const inputContent = ref("");

onMounted(() => {
  name.value = localStorage.getItem("name") || "";
  todos.value = JSON.parse(localStorage.getItem('todos')) || [];
});

const addTodo = () => {
  if(inputContent.value.trim() === "") {
    return;
  }
  
  todos.value.push({
    content: inputContent.value,
    done: false,
    createdAt: new Date().getTime()
  })
  
  inputContent.value = "";
};

const removeTodo = (todo) => {
  todos.value = todos.value.filter(t => t !== todo);
};

watch(todos, (newVal) => {
  localStorage.setItem('todos', JSON.stringify(newVal))
}, { deep: true });

watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

</script>

<style class="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 30px;
  background-color: lightgray;
}
</style>
