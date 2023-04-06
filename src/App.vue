<script setup>
import { ref } from 'vue';
import TodoList from './components/TodoList.vue'

const newTask = ref('')
const newNote = ref('')
const importance = ref('')
const newDate = ref('')
const todoItems = ref([])
let newID =  0


function onSubmit() {
  todoItems.value.push({
    task: newTask.value,
    note: newNote.value,
    importance: importance.value,
    date: newDate.value,
    done: false,
    id: newID++
  })
  newTask.value = ''
  newNote.value = ''
  importance.value = ''
  newDate.value = ''
}

function remove(id) {
  todoItems.value = todoItems.value.filter((i) => i.id !== id)
}

function toggleDone(id) {
  console.log(id)
  for (const todo of todoItems.value) {
    if (todo.id === id) {
      todo.done = !todo.done;
    }
  }
}
</script>

<template>
  <header>
    <div><h1><b>Track your Tasks</b></h1></div>
  </header>

  <main>
    <form @submit.prevent="onSubmit">
      <div class="row">
        <label for="task">Enter a Task </label>
        <input type="text" id="task"  required placeholder="Chop wood" v-model="newTask"/>
      </div>

      <div class="row">
        <label for="notes">Anything to note? </label>
        <input type="text" id="notes" placeholder="Carry water" v-model="newNote" />
      </div>

      <div class="row">
        <label for="importance">Priority </label>
        <select v-model="importance">
          <option disabled>Please select a level</option>
          <option>Low</option>
          <option>Medium</option>
          <option>High</option>
        </select>
      </div>

      <div class="row">
        <label for="date">Due date </label>
        <input type="date" v-model="newDate"/>
      </div>

      <button type="submit">Submit</button>

    </form>

    <div class="list">

      <h2><b>Todo List</b></h2>

      <TodoList v-for="todo in todoItems"
                      :key="todo.id"
                      :id="todo.id"
                      :task="todo.task"
                      :note="todo.note"
                      :importance="todo.importance"
                      :date="todo.date" 
                      :done="todo.done"
                      @toggle-done="toggleDone"
                      @remove="remove"
                      />

    </div>

    
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
  text-align: center;
  padding-bottom: 3rem;
}

.list > h2 {
  text-align: center;
  text-decoration: underline;
}

input {
  border-radius: 5px;
  border: 1px solid black;
}

select {
  border-radius: 5px;
  border: 1px solid black;
  background: white;
}

</style>
