<template>
  <div class="new-todo" :class="{ 'done-todo': item.done }">
    <input v-model="item.done" type="checkbox" class="checkbox"/>
    <label v-if="!inEditMode" @dblclick="edit">{{ item.title }}</label>
    <input v-focus class="edit" v-if="inEditMode" v-model="item.title" @keyup.enter="save"/>
    <button @click="$emit('deleteTodo', item)">x</button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ['item'],
  data: () => ({
    inEditMode: false
  }),
  methods: {
    edit() {
      this.inEditMode = true
    },
    save() {
      this.inEditMode = false
    }
  },
  directives: {
    focus: {
      inserted(el, binding) {
        el.focus()
      }
    }
  }
}
</script>

<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css?family=Raleway:500');

.new-todo {
  font-family: 'Raleway', sans-serif;
  width: 50%;
  font-size: 2rem;
  box-shadow: 0px 2px 10px rgba(0,0,0,0.2);
  margin: 20px auto;
  padding: 5px 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #ffffffcf;
  border-radius: 8px;
  transition: all 0.5s;
}

.edit {
  font-size: 2rem;
  padding: 0 10px;
  background-color: #ffffffcf;
  outline: none;
  border: 1px solid #009688;
  border-radius: 4px;
  text-align: center;
  color: #2c3e50;
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
  transition: background-color 0.5s;

  &:hover {
    background-color: #e31000;
  }
}

</style>
