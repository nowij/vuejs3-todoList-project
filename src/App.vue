<template>
  <!-- 줄여쓰기 v-bind: = :class -->
  <!-- 줄여쓰기 v-on:   = @      -->
  <div class="container">
    <h2>To-Do LIST</h2>
    <form @submit.prevent="onSubmit">
      <div class="d-flex">
        <!-- 입력창 -->
        <div class="flex-grow-1 mr-2">
          <input class="form-control" type="text" v-model="todo" placeholder="Type new to-do" >
        </div>
        <div>
          <button class="btn btn-primary" type="submit"> Add </button> 
        </div>
      </div>
    </form>
    <!-- 빈 값 입력 시 -->
    <div v-if="hasError" style="color: red;">
      This filed cannot be Empty!
    </div>
    <div v-for="(todo, index) in todoList" :key="todo.id">
      <div class="card mt-2">
        <div class="card-body p-2 d-flex aline-items-center">
          <!-- 목록 -->
          <div class="form-chekck flex-grow-1">
            <input class="form-cheeck-input" type="checkbox" v-model="todo.completed"/>
            <label class="form-check-label" :class="{ todo: todo.completed }">{{ todo.subject }}</label>
          </div>
          <!-- 삭제 -->
          <div>
            <button class="btn btn-danger btn-sm" @click="deleteTodo(index)">Delete</button>
          </div>
        </div>
      </div>
    </div>
    
</div>

</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const todo = ref('');
    const todoList = ref([]);
    const hasError = ref(false);

    const onSubmit = (e) => {
      e.preventDefault();
      if (todo.value === '') {
        hasError.value = true;
      } else {
        todoList.value.push({
            id: Date.now(),
            subject: todo.value,
            completed: false
        });
        hasError.value = false;
        todo.value = ''; // 입력창 clear
      }
    };

    const deleteTodo = (index) => {
      todoList.value.splice(index, 1);
    };

    return {
      todo, 
      onSubmit,
      todoList,
      hasError,
      deleteTodo
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
