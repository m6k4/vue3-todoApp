<template>
  <div class="list">
      <h2> Todo App </h2>
      <form @submit.prevent="addTodo">
      <input v-model="description">
      {{description}}
      <button > Add new task </button>
      </form>
    <div v-for="todo in todos" v-bind:key="todo.description">
        Status: {{todo.status ? 'Done' : 'To do'}} Description: {{todo.description}}
        <button @click="makeItDone(todo)"> Toggle status </button>
    </div>
  </div>
</template>

<script>
import { ref, reactive } from 'vue'
export default {
  name: 'TodoList',

  setup () {
    const description = ref('')
    const todos = reactive([])

    function addTodo () {
      todos.push({
        done: 'false',
        description: description.value
      })
      description.value = ''
    }
    function makeItDone (todo) {
      todo.status = !todo.status
    }
    return { description, addTodo, todos, makeItDone }
  }
}
</script>
