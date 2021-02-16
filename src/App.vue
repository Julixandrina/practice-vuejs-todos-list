<template>
  <div id="app">
    <application-layout>
      <template v-slot:header>
        <!-- As a heading -->
        <nav class="navbar navbar-light bg-light">

<span class="navbar-brand mb-0 h1">Navbar</span>
</nav>
      </template>

      <template v-slot:default>
        <h1 class=" text-center">To do app</h1>
        <div class="container-actions">
          <input-new-item
              v-on:add-todo="addTodo"
          ></input-new-item>

          <div class="btns-box">
             <button-toggle-checked
              v-show="!loading"
              v-on:btn-toggle-checked="toggleCheckedAll"
          >
            <icon-button-toggle></icon-button-toggle>
            Select all
          </button-toggle-checked>

          <button-remove-completed
              v-show="computed.length > 0"
              v-on:remove-completed="removeCompleted"
          >Delete
          </button-remove-completed>
          </div> 
          </div>

        <select class="custom-select custom-select-sm w-50"
                v-model="filter"
                v-show="!loading">
          <option value="all">All</option>
          <option value="completed">Completed</option>
          <option value="active">Active</option>
        </select>


        <loader-preview v-if="loading"></loader-preview>


        <todo-list
            v-bind:todos="filteredTodos"
            @remove-todo="removeTodo"
            v-else-if="filteredTodos.length"
            class="list-tasks"
        >
        </todo-list>

        <p v-else>Tasks empty!</p>
      </template>

      <template v-slot:footer>

      <div class="container  text-center">
    <span class="text-muted">Thank you for review</span>
  </div>

       
       
      </template>
    </application-layout>
  </div>
</template>

<script>
import AppLayout from "@/components/AppLayout"
import TodoList from "@/components/TodoList"
import TodoListItemAdd from "@/components/TodoListItemAdd"
import Loader from "@/components/Loader"
import TodoListBtnDelCompleted from "@/components/TodoListBtnDelCompleted"
import TodoListBtnToggleChecked from "@/components/TodoListBtnToggleChecked"
import Icon from "@/components/Icon"


export default {
  name: 'App',
  components: {
    'todo-list': TodoList,
    'input-new-item': TodoListItemAdd,
    'loader-preview': Loader,
    'button-remove-completed': TodoListBtnDelCompleted,
    'button-toggle-checked': TodoListBtnToggleChecked,
    'icon-button-toggle': Icon,
    'application-layout': AppLayout,

  },
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos
      }
      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed);
      }
      if (this.filter === 'active') {
        return this.todos.filter(t => !t.completed);
      }
    },
    active: function () {
      return this.todos.filter(function (task) {
        return !task.completed;
      });
    },
    computed: function () {
      return this.todos.filter(function (task) {
        return task.completed;
      });
    },

  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos/')
        .then(response => response.json())
        .then(json => {
          setTimeout(() => {
                this.todos = json.slice(0, 3)
                this.loading = false
              }, 1000
          )
        })
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(newTodo) {
      this.todos.splice(0, 0, newTodo);
    },
    removeCompleted() {
      this.todos = this.active;
    },

    toggleCheckedAll(isOneNotCheckedFound) {
      this.todos.forEach(function (todo) {
        if (todo.completed === false) {
          isOneNotCheckedFound = true;
        }
      })
      if (isOneNotCheckedFound) {
        return this.todos.forEach(function (todo) {
          todo.completed = true

        })
      } else {
        return this.todos.forEach(function (todo) {
          todo.completed = false
        })
      }
    }
  }
}
</script>
<style scoped>
.btns-box {
  display: flex;
}
.container-actions {
  padding: 1rem 0;
  margin-bottom: 1rem;
}
.list-tasks {
  padding: 1rem 0;
}


</style>



