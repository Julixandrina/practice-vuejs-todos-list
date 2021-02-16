<template>
  <div>
    <ul class="list-group">
      <todo-list-item
      v-for="todo in todos"
      v-bind:todo="todo"
      v-bind:key="todo.id"
      v-bind:id="todo.id"
      v-on:remove-todo="removeTodo"
      >
      </todo-list-item>
    </ul>
  </div>
</template>

<script>
import TodoListItem from "@/components/TodoListItem";

export default {
  name: "TodoList",
  props: ['todos'],
  components: {
    'todo-list-item': TodoListItem,
  },
  methods: {
    removeTodo(id) {
      this.$emit('remove-todo', id)
    },

  },
}
</script>
