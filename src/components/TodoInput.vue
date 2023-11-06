<template>
  <section class="create-todo">
    <h3>Create a todo.</h3>

    <form @submit.prevent="addTodo">
      <input type="text" placeholder="write" :value="inputContent" @input="inputContentHandler($event)" />
      <button type="submit">ADD</button>
    </form>
  </section>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits, Ref } from "vue";

const props: { inputContent: Ref; addTodo: Function } = defineProps([
  "inputContent",
  "addTodo",
]);

const emit = defineEmits(["addTodo"]);

const inputContentHandler = (event: Event) => {
  console.log("e: ", props.inputContent)
  // props.inputContent = event.target.value;
}

</script>
