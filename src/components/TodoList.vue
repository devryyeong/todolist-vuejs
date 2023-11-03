<template>
  <section class="todo-list">
    <h3>TODO LIST</h3>
    <div class="list">
      <div v-for="todo in todos" :class="`todo-item ${todo.done && 'done'}`" :key="todo.content">
        <label>
          <input type="checkbox" v-model="todo.done">
        </label>

        <span class="todo-content">
          <input type="text" v-model="todo.content">
        </span>
        <span>
          <button class="delete" @click="removeTodo(todo)">Delete</button>
        </span>
      </div>
    </div>
  </section>
</template>
<script lang="ts" setup>
const props = defineProps<{
  todos: any[]
}>();

</script>
<style lang="">
  
</style>