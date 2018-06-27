<template>
  <form @submit.prevent="addItem">
    <input v-model.trim="newItem" placeholder="What needs to be done?">
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
@import url('https://fonts.googleapis.com/css?family=Raleway:500');

form {
  font-family: 'Raleway', sans-serif;
}

  input {
    width: 60%;
    margin: 220px 15px 50px 15px;
    padding: 10px 15px;
    font-size: 2em;
    border-radius: 4px;
    color: #3e5a68;
    border: 1px solid #000;
    outline: none;
    background: #ffffffc4;
  }
</style>
