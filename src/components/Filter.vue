<template>
  <div class="filters">
    <ul class="breadcrumbs">
      <li class="filter" :class="{ active: isFiltered('all') }" @click="$emit('filter', all)">All</li>
      <li class="filter" :class="{ active: isFiltered('active') }" @click="$emit('filter', active)">Active</li>
      <li class="filter" :class="{ active: isFiltered('done') }" @click="$emit('filter', done)">Done</li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'TodoFilter',
    data: () => ({
      currentFilter: 'all'
    }),
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
      }
    }
  }
</script>
