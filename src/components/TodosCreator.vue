<script setup>
import { defineEmits, reactive } from 'vue';
import TodoButton from './TodoButton.vue';

const todoState = reactive({
  todo: "",
  invalid: null,
  errMsg:""
});
const emit = defineEmits(['create-todo']);

const createTodo = () => {
  todoState.invalid = null;
  if (todoState.todo !== "") {
    emit('create-todo', todoState.todo);
    todoState.todo = "";
    return;
  }
  todoState.invalid = true;
  todoState.errMsg = "Todo value cannot be empty";
}
</script>


<template>
  <div class="input-wrap" :class="{'input-err':todoState.invalid}">
  <input type="text" v-model="todoState.todo"/>
  <TodoButton @click="createTodo()">Create</TodoButton>
  </div>
<p v-show="todoState.invalid" class="err-msg" >{{ todoState.errMsg }}</p>

</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;
  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }
  &.input-err{
  border-color: red;

}


  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }
}
.err-msg{
  text-align: center;
  color: red;
  margin-top: 5px;
  font-size: 12px;
}
</style>