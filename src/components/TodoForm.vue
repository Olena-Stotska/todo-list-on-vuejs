<template>
  <form @submit.prevent="addItem">
    <input @input="emitValue" v-model.trim="newItem" placeholder="What needs to be done?">
  </form>
</template>

<script>
  export default {
    name: 'TodoForm',
    props: ['value'],
    data: () => ({
      newItem: '',
    }),
    watch: {
      value(value) {
        this.newItem = value
      }
    },
    methods: {
      addItem() {
        this.$emit('newTodo', { title: this.newItem, done: false, id: Math.random() })
        this.newItem = ''
      },
      emitValue() {
        clearTimeout(this.timerId)
        this.timerId = setTimeout(() => this.$emit('input', this.newItem), 100)
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

    &::placeholder {
      color: #b5b5b5bf;
    }
  }
</style>
