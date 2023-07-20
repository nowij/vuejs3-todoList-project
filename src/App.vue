<template>
  <!-- 줄여쓰기 v-bind: = :class -->
  <!-- 줄여쓰기 v-on:   = @      -->
  <div class="container">
    <h2>To-Do LIST</h2>
    <TodoSimpleForm @add-todo="addTodo"/>
    <TodoList :todoList="todoList"
      @toggle-todo="toggleTodo"
      @delete-todo="deleteTodo"/>
</div>

</template>

<script>
import { ref } from 'vue';
import TodoSimpleForm from './components/TodoSimpleForm.vue';
import TodoList from './components/TodoList.vue';

export default {
  // 컴포넌트 등록
  components: {
    TodoSimpleForm,
    TodoList
  },

  setup() {
    const todoList = ref([]);

    const addTodo = (todo) => {
      todoList.value.push(todo);
    };

    const deleteTodo = (index) => {
      console.log(index);
      todoList.value.splice(index, 1);
    };

    const toggleTodo = (index) => {
      todoList.value[index].completed = !todoList.value[index].completed;
    }

    return {
      todoList,
      addTodo,
      deleteTodo,
      toggleTodo
    };
  }
}
</script>

<style>
  .todo {
    color: gray;
    text-decoration: line-through;
  }
</style>
