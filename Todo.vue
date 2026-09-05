<script setup>
import { ref } from 'vue'

const newTodo = ref('')
const count = ref(0)

function increment() {
  count.value += 1  // ใน script ใช้ .value
}
</script>

<template>
    <!-- template แกะ .value ให้อัตโนมัติ -->
  <p>{{ count }}</p>
  
  <button class="todo-btn" @click="increment">เพิ่มจำนวน</button>
</template>

<style scoped>
.todo-btn {
  background-color: #42b983; 
  color: white; 
  font-size: 1.5rem; 
  font-weight: bold; 
  font-family: sans-serif;
  padding: 10px 30px; 
  border: none; 
  border-radius: 8px; 
  cursor: pointer; 
  transition: background-color 0.2s ease;
}


.todo-btn:hover {
  background-color: #33a06f; 
}
</style>