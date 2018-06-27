<template>
  <div class="filters">
    <ul class="breadcrumbs">
      <li class="filter" :class="{ active: isFiltered(all) }" @click="setActiveFilter(all)">All</li>
      <li class="filter" :class="{ active: isFiltered(active) }" @click="setActiveFilter(active)">Active</li>
      <li class="filter" :class="{ active: isFiltered(done) }" @click="setActiveFilter(done)">Done</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TodoFilter',
  data() {
    return { currentFilter: this.all }
  },
  methods: {
    isFiltered(name) {
      return this.currentFilter === name
    },

    all(items) {
      return items
    },

    active(items) {
      return items.filter(item => !item.done)
    },

    done(items) {
      return items.filter(item => item.done)
    },
    setActiveFilter(filter) {
      this.currentFilter = filter
      this.$emit('filter', filter)
    }
  }
}
</script>

<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css?family=Raleway:500');

.filters {
  font-family: 'Raleway', sans-serif;
  padding: 0;
  display: flex;
  justify-content: center;
  list-style-type: none;
}

ul {
  list-style: none;
  display: flex;
  justify-content: center;
  margin: 0;
}

li {
  margin: 0 15px;
  cursor: pointer;
  padding: 2px 10px;
  color: #009688;
  font-size: 1.52rem;
}

.active {
  font-weight: bold;
  text-shadow: 1px 4px 4px rgba(0, 0, 0, 0.4);
  transition: all 0.5s;
  border-bottom: 1px solid #9E9E9E;
}
</style>
