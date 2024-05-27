<script>
import TodoTable from "./TodoTable.vue";

export default {
      components: {
            TodoTable
      },
      data() {
            return {
                  todo: '', // Assuming defineModel was meant to be a reactive property for the todo input
                  todos: []
            };
      },
      methods: {
            addTodo() {
                  this.todos.push(this.todo);
                  localStorage.setItem("todos", JSON.stringify(this.todos));
                  this.todo = ''; // Clear the input after adding a todo
            },
            async getTodos() {
                  try {
                        const storedData = localStorage.getItem("todos");
                        if (storedData) {
                              this.todos = JSON.parse(storedData);
                        } else {
                              this.todos = [];
                        }
                  } catch (error) {
                        console.error("Failed to fetch todos:", error);
                        this.todos = [];
                  }
            }
      },
      mounted() {
            this.getTodos();
      }
}
</script>

<template>
      <div class="">
            <div class="card">
                  <div class="card-body">
                        <h3 class="card-title lead text-primary fw-bold">Todo Form</h3>
                        <div class="">
                              <form class="v-stack" @submit.prevent="addTodo">
                                    <input type="text" class="form-control" placeholder="Write here..."
                                          v-model="todo" />
                                    <button class="btn btn-primary my-2" type="submit">Create</button>
                              </form>
                        </div>
                        <div class="">
                              <TodoTable :todos="todos" />
                        </div>
                  </div>
            </div>
      </div>
</template>