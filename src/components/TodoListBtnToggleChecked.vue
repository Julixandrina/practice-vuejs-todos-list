<template>
  <div>
    <button type="button" class="btn btn-light btn-checked" v-on:click="ToggleChecked">
            <slot></slot>
    </button>
  </div>
</template>

<script>


export default {
  name: "TodoListBtnToggleChecked",
  components: {

  },
  data() {
    return {
      isOneNotCheckedFound: false,

    }
  },
  methods: {
    ToggleChecked() {
      this.$emit('btn-toggle-checked', this.isOneNotCheckedFound)
    }
  }
}
</script>

<style scoped>
.btn-checked {
  display: flex;
  align-items: center;
  margin-right: 0.5rem;
}

</style>