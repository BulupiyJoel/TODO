<script setup>
import { onMounted, ref } from 'vue'
import TodoButton from "../TodoButtons/TodoButton.vue"
import TodoIcon from "../TodoButtons/TodoIcon.vue"

let todos = ref([]); // Initialize as an empty array for storing todos
let emptyTodosMessage = "There is no todo in the database";

// Values
let title = ref(''); // For the new todo input
let selectedTodo = ref(null); // For storing the selected todo

// Methods
const addTodo = () => {
      // Create a new todo item with a unique id and the title from input
      const newTodo = {
            id: todos.value.length + 1, // Simple ID assignment (you might want a more robust method in a real app)
            title: title.value
      };
      todos.value.push(newTodo); // Add the new todo to the list
      localStorage.setItem("todos", JSON.stringify(todos.value)); // Update localStorage
      title.value = ""; // Clear the input after adding a todo
};

const clearTodos = () => {
      localStorage.removeItem("todos"); // Clear todos from localStorage
      todos.value = []; // Reset the todos array
};

const getTodos = async () => {
      try {
            const storedData = localStorage.getItem("todos");
            if (storedData) {
                  todos.value = JSON.parse(storedData); // Load todos from localStorage
            } else {
                  console.log("No data in localStorage");
            }
      } catch (error) {
            console.error("Failed to fetch todos:", error);
            todos.value = []; // Reset todos if there's an error
      }
};

const editTodo = (todo) => {
      selectedTodo.value = todo; // Store the selected todo
      title.value = todo.title; // Set the input value to the selected todo's title
};

const updateTodo = () => {
      if (selectedTodo.value) {
            selectedTodo.value.title = title.value; // Update the selected todo's title
            selectedTodo.value = null; // Reset the selected todo
            title.value = ""; // Clear the input
            localStorage.setItem("todos", JSON.stringify(todos.value)); // Update localStorage
      }
};

onMounted(() => {
      getTodos();
});

</script>
<template>
      <div class="d-flex flex-column gap-3">

            <div class="">
                  <div class="card">
                        <div class="card-body">
                              <h3 class="card-title lead text-primary fw-bold">Todo Form</h3>
                              <div class="">
                                    <!--Creation-Form-->
                                    <form class="v-stack" @submit.prevent="addTodo">
                                          <input type="text" class="form-control" placeholder="Write here..."
                                                v-model="title" />
                                          <div class="">
                                                <button class="btn btn-primary my-2 w-100" type="submit">
                                                      Create <i class="bi bi-plus-circle"></i>
                                                </button>
                                          </div>
                                    </form>
                                    <!--Edition-Form-->

                              </div>
                        </div>
                  </div>
            </div>
            <div class="p-3 rounded" v-if="todos.length !== 0">

                  <div class="d-flex flex-column gap-3">
                        <h2 class="lead">My todos</h2>
                        <div class="col-6">
                              <button class="btn btn-danger my-2" @click="clearTodos()">
                                    <i class="bi bi-trash"></i> Clear Table
                              </button>
                        </div>
                  </div>
                  <table class="table">
                        <thead>
                              <tr>
                                    <th class="col">#</th>
                                    <th scope="col">Title</th>
                                    <th scope="col">Actions</th>
                              </tr>
                        </thead>
                        <tbody>
                              <tr v-for="todo in todos" :key="todo.id">
                                    <th>{{ todo.id }}</th>
                                    <th>{{ todo.title }}</th>
                                    <td class="">
                                          <div class="row d-flex justify-content-start">
                                                <div class="col-4">
                                                      <form @submit.prevent>
                                                            <input type="hidden" v-model="todo.id">
                                                            <TodoButton className="btn btn-primary" label="Edit"
                                                                  @click="editTodo(todo)">
                                                                  <TodoIcon iconClass="bi bi-pen" />
                                                            </TodoButton>
                                                      </form>
                                                </div>
                                                <div class="col-4">
                                                      <TodoButton className="btn btn-success" label="Update"
                                                            @click="updateTodo">
                                                            <TodoIcon iconClass="bi bi-check2" />
                                                      </TodoButton>
                                                </div>
                                          </div>
                                    </td>
                              </tr>
                        </tbody>
                  </table>
            </div>
            <div class="alert alert-info" v-else>
                  <h4 class="alert-heading">Warning!</h4>
                  <hr />
                  <p class="mb-0">{{ emptyTodosMessage }} <i class="bi bi-database"></i></p>
            </div>
      </div>
</template>