<template>
  <li class="list-group-item">
    <span>
      <base-checkbox
          v-model="todo.completed"></base-checkbox>
     <!-- <input type="checkbox" v-on:change="toggleStatusChecked(todo)" v-model="todo.completed">-->
      <span class="ml-2 mr-2" v-bind:class="{done: todo.completed}">{{todo.title | uppercase}} </span>




    </span>




    <button type="button"
            class="btn btn-outline-primary"
            v-on:click="$emit('remove-todo', todo.id)">&times;
    </button>
  </li>

</template>

<script>
import BaseCheckbox from "@/components/BaseCheckbox"
export default {
name: "TodoListItem",
  components: {
    'base-checkbox': BaseCheckbox
  },
  props: {
  todo: {
    type: Object,
    required: true,
  }
  },
  filters: {
  uppercase(value) {
    return value.toUpperCase()
  }
  },
  methods: {
    /*toggleStatusChecked: function (todo) {
      todo.statusChecked = !todo.statusChecked;
    }*/
  }

}
</script>

<style scoped>
.list-group-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.done {
  text-decoration: line-through;
}
.active-plan {
  color: red;
}
</style>