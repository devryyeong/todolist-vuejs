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
          <input
            type="checkbox"
            :value="todo.done"
            @change="checkboxHandler(todo, $event)"
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
    // type: Object as PropType<TodoItem>,
    type: Array as PropType<Array<TodoItem>>,
    // type: String as PropType<'ITEM'|'LIST'>,
    // type: Array<TodoItem>,
    required: true,
  },
});

const emit = defineEmits<{
  removeTodo: [TodoItem];
  updateTodo: [TodoItem];
}>();

const checkboxHandler = (todo: TodoItem, event: Event) => {
  const updatedTodo = { ...todo };
  updatedTodo.done = event.target?.checked;
  emit("updateTodo", updatedTodo);
};

const contentHandler = (todo: TodoItem, event: Event) => {
  const updatedTodo = { ...todo };
  updatedTodo.content = event.target?.value;
  emit("updateTodo", updatedTodo);

};

</script>

<style></style>
