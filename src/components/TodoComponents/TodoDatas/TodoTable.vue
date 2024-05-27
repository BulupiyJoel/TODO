<script setup>
import TodoButton from "../TodoButtons/TodoButton.vue"
defineProps({
      todos : {
            required : true
      } 
})

</script>
<template>
      <table class="table">
            <thead>
                  <tr>
                        <th scope="col">Title</th>
                        <th scope="col">Actions</th>
                  </tr>
            </thead>
            <tbody>
                  <tr>
                        <th>{{ todos }}</th>
                        <td>
                              <TodoButton className="btn btn-primary" label="Edit"/>
                              <TodoButton className="btn btn-danger" label="Delete"/>
                        </td>
                  </tr>
            </tbody>
      </table>
</template>