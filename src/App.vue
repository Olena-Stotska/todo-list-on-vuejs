<template>
  <div id="app">
    <TodoForm @newTodo="addTodo" />
    <TodoItem @deleteTodo="deleteTodo" :item="item" v-for="item in filteredItems"/>
    <TodoFilter @filter="setFilter" />
  </div>
</template>

<script>
import TodoForm from './components/TodoForm';
import TodoItem from './components/TodoItem';
import TodoFilter from './components/Filter';

export default {
  name: 'app',
  components: {
    TodoForm,
    TodoItem,
    TodoFilter
  },
  data: () => ({
    items: [],
    currentFilter: items => items
  }),
  computed: {
    filteredItems() {
      return this.currentFilter(this.items)
    }
  },
  methods: {
    addTodo(todo) {
      this.items.push(todo)
    },
    deleteTodo(todo) {
      const indexTodo = this.items.indexOf(todo)
      this.items.splice(indexTodo, 1)
    },
    setFilter(fn) {
      this.currentFilter = fn
    }
  }
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Galada');

#app {
  font-family: 'Galada', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 18px;

  &:after {
    content: 'Todos';
    font-size: 24em;
    color: #a8c8c5;
    font-weight: bold;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    z-index: -1;
  }
}

</style>
