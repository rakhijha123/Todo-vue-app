<template>
  <div class="wrapper">
    <header>Todo App</header>
   
      <form @submit.prevent="addTodo" class="inputField">
        <input v-model="newTodo" placeholder="Add your new todo" />
        <button type="submit"><i class="ri-add-line"></i></button>
      </form>
  
    <ul class="todoList">
      <li v-for="(todo, index) in todos" :key="index">
        {{ todo.text }}<span><button @click="deleteTodo(index)"><i class="ri-delete-bin-6-fill"></i></button></span>
      </li>

      <!-- <li>complete a previous task<span><button>delete</button></span></li>
        <li>create a video for utube<span><button>delete</button></span></li>
        <li>create a new portfolio site<span><button>delete</button></span></li> -->
    </ul>
    <div class="footer">
      <span>you have {{ remainingTasks }} pending task</span>
      <button @click="clearAll">Clear All</button>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";

//Data
const todos = ref([
  // { text: "", completed: true },
  // { text: "", completed: true },
]);

const newTodo = ref("");

const remainingTasks = ref(todos.value.length);

//methods
const addTodo = () => {
  if (newTodo.value.trim() !== "") {
    todos.value.push({ text: newTodo.value, completed: false });
    newTodo.value = "";
    updateRemainingTasks();
  }
};
const deleteTodo = (index) => {
  todos.value.splice(index, 1);
  updateRemainingTasks();
};

const clearAll = () => {
  todos.value = [];
  updateRemainingTasks();
};

// Function to update the remaining tasks count
const updateRemainingTasks = () => {
  remainingTasks.value = todos.value.length;
};
</script>
