<template>
  <form @submit.prevent="addItem">
    <input v-model.trim="newItem" placeholder="Enter Input">
  </form>
</template>

<script>
  export default {
    name: 'TodoForm',
    data: () => ({
      newItem: '',
    }),
    methods: {
      addItem() {
        this.$emit('newTodo', { title: this.newItem, done: false })
        this.newItem = ''
      }
    }
  }
</script>

<style scoped lang="scss">

</style>
