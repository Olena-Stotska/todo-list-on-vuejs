<template>
  <div>
    <input v-model="item.done" type="checkbox" :class="{ done: item.done }" />
    {{ item.title }}
    <button @click="$emit('deleteTodo', item)">x</button>
  </div>
</template>

<script>
  export default {
    name: "TodoItem",
    props: ['item']
  }
</script>
