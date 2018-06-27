<template>
  <div class="new-todo" :class="{ 'done-todo': item.done }">
    <input v-model="item.done" type="checkbox" class="checkbox" :class="{ done: item.done }" />
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

<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css?family=Raleway:500');

.new-todo {
  font-family: 'Raleway', sans-serif;
  width: 50%;
  font-size: 2.5rem;
  box-shadow: 0px 2px 10px rgba(0,0,0,0.2);
  margin: 20px auto;
  padding: 0 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #ffffffcf;
  border-radius: 8px;
  transition: all 1s;
}

.done-todo {
  text-decoration: line-through;
  color: #bcbcbcd1;
}

.checkbox {
  -webkit-appearance: none;
  background-color: #fafafa;
  border: 1px solid #cacece;
  box-shadow: 0 1px 2px rgba(0,0,0,0.05), inset 0px -15px 10px -12px rgba(0,0,0,0.05);
  padding: 9px;
  border-radius: 3px;
  display: inline-block;
  position: relative;
  outline: none;
  cursor: pointer;
  transition: all 1s;

  &:active, &:checked:active {
    box-shadow: 0 1px 2px rgba(0,0,0,0.05), inset 0px 1px 3px rgba(0,0,0,0.1);
  }

  &:checked {
    background-color: #e9ecee;
    border: 1px solid #adb8c0;
    box-shadow: 0 1px 2px rgba(0,0,0,0.05), inset 0px -15px 10px -12px rgba(0,0,0,0.05), inset 15px 10px -12px rgba(255,255,255,0.1);
    color: #99a1a7;
  }

    &:checked:after {
    content: '\2714';
    font-size: 2em;
    position: absolute;
    top: -7px;
    left: -1px;
    color: #607D8B;
  }
}

button {
  border: none;
  font-size: 1.2rem;
  color: #fff;
  font-weight: bold;
  background-color: #e5c8c8;
  border-radius: 50%;
  outline: none;
  cursor: pointer;
  transition: background-color 1s;

  &:hover {
    background-color: #e31000;
  }
}

</style>
