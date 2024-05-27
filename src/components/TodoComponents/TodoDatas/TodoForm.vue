<script setup>
import TodoTable from "./TodoTable.vue";

let todo = defineModel()
let todos = [];
function addTodo() {
      todos.push(todo)
      let stored = todos
      localStorage.setItem("todos", stored)
}
let getTodos = () => {
      return localStorage.getItem("todos")
}

// function deleteTodo() {
//       localStorage.removeItem("todos")
// }

</script>

<template>
      <div class="">
            <div class="card">
                  <div class="card-body">
                        <h3 class="card-title lead text-primary fw-bold">Todo Form</h3>
                        <div class="">
                              {{ todo + " | " + todos }}
                              <form class="v-stack" @submit.prevent>
                                    <input type="text" name="" id="" class="form-control" placeholder="Write here..."
                                          v-model="todo">
                                    <button class="btn btn-primary my-2" @click="addTodo">Create</button>
                              </form>
                        </div>
                        <div class="">
                              <TodoTable :todos="getTodos()"/>
                        </div>
                  </div>
            </div>
      </div>
</template>