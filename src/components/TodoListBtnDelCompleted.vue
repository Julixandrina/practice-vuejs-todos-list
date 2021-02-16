<template>
<div>


  <button type="button" class="btn btn-outline-danger" v-on:click="removeCompleted"><slot></slot></button>
</div>
</template>

<script>
export default {
name: "TodoListBtnDelCompleted",
methods: {
  removeCompleted() {
    this.$emit('remove-completed')
  }

}
}
</script>

<style scoped>

</style>