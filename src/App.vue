<script setup>
import { ref } from 'vue'

const newTodo = ref('')
const todos = ref([
  { id: 1, text: 'Learn Vue', done: false },
  { id: 2, text: 'Build a todo app', done: true }
])

function addTodo() {
  const text = newTodo.value.trim()
  if (!text) return

  todos.value.push({
    id: Date.now(),
    text,
    done: false
  })
  newTodo.value = ''
}

function toggleTodo(id) {
  todos.value = todos.value.map((todo) =>
    todo.id === id ? { ...todo, done: !todo.done } : todo
  )
}

function removeTodo(id) {
  todos.value = todos.value.filter((todo) => todo.id !== id)
}
</script>

<template>
  <main class="app">
    <h1>Todo App</h1>

    <form class="todo-form" @submit.prevent="addTodo">
      <input v-model="newTodo" placeholder="Add a new task" />
      <button type="submit">Add</button>
    </form>

    <ul class="todo-list">
      <li v-for="todo in todos" :key="todo.id" :class="{ done: todo.done }">
        <label>
          <input type="checkbox" :checked="todo.done" @change="toggleTodo(todo.id)" />
          <span>{{ todo.text }}</span>
        </label>
        <button class="remove" @click="removeTodo(todo.id)">Delete</button>
      </li>
    </ul>
  </main>
</template>

<style scoped>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f4f7fb;
}

.app {
  max-width: 540px;
  margin: 60px auto;
  padding: 24px;
  background: white;
  border-radius: 14px;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.08);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.todo-form {
  display: flex;
  gap: 10px;
  margin-bottom: 18px;
}

.todo-form input {
  flex: 1;
  padding: 10px 12px;
  border: 1px solid #d5dbe3;
  border-radius: 8px;
}

.todo-form button,
.remove {
  border: none;
  border-radius: 8px;
  background: #42b883;
  color: white;
  cursor: pointer;
}

.todo-form button {
  padding: 10px 16px;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 10px;
  border-bottom: 1px solid #eef2f5;
}

.todo-list label {
  display: flex;
  align-items: center;
  gap: 10px;
  flex: 1;
}

.todo-list .done span {
  text-decoration: line-through;
  color: #9098a7;
}

.remove {
  padding: 8px 10px;
  background: #e74c3c;
}
</style>
