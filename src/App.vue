<script setup>
import { computed, ref } from "vue";

let id = 0;
const hideCompleted = ref(false);
const newTodo = ref("");
const todos = ref([]);

function addTodo() {
  todos.value.push({
    id: id++,
    text: newTodo.value,
    done: false,
  });
  newTodo.value = "";
}

function removeTodo(todo) {
  const index = todos.value.indexOf(todo);
  if (index > -1) {
    todos.value.splice(index, 1);
  }
}

const filterTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((todo) => !todo.done)
    : todos.value;
});
</script>

<template>
  <center>
    <form @submit.prevent="addTodo">
      <input v-model="newTodo" required placeholder="new todo" />
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in filterTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done" />
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? "Show all" : "Hide completed" }}
  </button>
</center>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
