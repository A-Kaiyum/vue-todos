<script setup>
import TodosCreator from '../components/TodosCreator.vue';
import { Icon } from "@iconify/vue";
import { ref } from "vue";
import { uid } from "uid";
import TodoItem from '../components/TodoItem.vue';
const todoList = ref([]);
const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};
const toggleCompleted = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
}
const todoEdit = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
}
const todoUpdate = (todoVal, todoPos) => {
  console.log(todoVal);
  todoList.value[todoPos].todo = todoVal;
}
const todoDelete = (todoId) => {
  todoList.value = todoList.value.filter((todo)=>todo.id !== todoId)
}
</script>

<template>
  <main>
    <h1>Create Todos</h1>
    <TodosCreator @create-todo="createTodo"/>
    <ul class="todo-list" v-if="todoList.length>0">
      <TodoItem v-for="(todo,index) in todoList" 
      :todo="todo" :index="index" 
      @toggle-complete="toggleCompleted" 
      @edit-todo="todoEdit"
      @update-todo="todoUpdate"
      @delete-todo="todoDelete"
       />
    </ul>
    <p class="todos-msg" v-else>
          <Icon  icon="noto-v1:sad-but-relieved-face" class="icon" width="22"/>
          <span>You have no todos to complete! Add one!</span>
    </p>
  </main>
</template>
<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
}
 .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
</style>