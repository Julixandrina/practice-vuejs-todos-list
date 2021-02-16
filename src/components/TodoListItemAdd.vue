<template>
  <form v-on:submit.prevent="saveNewItem">
    <input type="text" class="form-control" v-model.trim="title">
    <button type="submit" class="btn btn-primary mt-2 mb-2">Add</button>
  </form>
</template>

<script>
export default {
  name: "TodoListItemAdd",
  data() {
    return {
      title: '',
      uniqueId: Date.now(),
    }
  },
  methods: {
    saveNewItem() {
      if (!this.title) {
        return
      }
      let newTodo = {
        id: `${'t' + this.uniqueId++}`,
        title: this.title,
        completed: false
      }
      this.$emit('add-todo', newTodo)
      this.title = ''

    }
  },

}
</script>

<style scoped>

</style>