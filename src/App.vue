<template>
  <div id="app">
    <TodoForm @newTodo="addTodo" v-model="search" />
    <TodoFilter @filter="setFilter" />
    <transition-group :name="animation">
      <TodoItem @deleteTodo="deleteTodo" :key="item.id" :item="item" v-for="item in filteredItems"/>
    </transition-group>
  </div>
</template>

<script>
import TodoForm from './components/TodoForm';
import TodoItem from './components/TodoItem';
import TodoFilter from './components/Filter';
const STORAGE_KEY = 'todoList-vuejs'

export default {
  name: 'app',
  components: {
    TodoForm,
    TodoItem,
    TodoFilter
  },
  data: () => ({
    items: JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'),
    currentFilter: items => items,
    animation: '',
    search: '',
  }),
  computed: {
    filteredItems() {
      const items = this.currentFilter(this.items)
      const term = this.search.toLowerCase()

      if (!term) {
        return items
      }

      return items.filter(item => item.title.toLowerCase().includes(term))
    }
  },
  watch: {
    filteredItems(newItems, oldItems) {
      this.animation = newItems.length >= oldItems.length ? 'add' : 'remove'
    },
    items: {
      handler() {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(this.items))
      },
      deep: true
    }
  },
  methods: {
    addTodo(todo) {
      this.search = ''
      this.$nextTick(() => {
        this.items.push(todo)
      })
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
@import './animation/animation.scss';

.remove-enter,
.remove-leave-to {
  animation: fadeInLeft 0.6s;
}

.remove-enter-active,
.remove-leave-active {
  animation: fadeOutLeft 0.6s;
}

.add-enter,
.add-leave-to {
  animation: fadeOutLeft 0.6s;
}

.add-enter-active,
.add-leave-active {
  animation: fadeInLeft 0.6s;
}

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
