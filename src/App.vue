<template>
<!-- 줄여쓰기 v-bind: = :class -->
<!-- 줄여쓰기 v-on: = @        -->
<div class="container">
    <h2>To-Do LIST</h2>
    <form class="d-flex" @submit="onSubmit">
      <div class="flex-grow-1 mr-2">
        <input class="form-control" type="text"
          v-model="todo" placeholder="Type new to-do" >
      </div>
      <div>
        <button
          class="btn btn-primary"
          type="submit"> Add
        </button>   
      </div>
    </form>
    {{todoList}}
</div>
  
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const todo = ref('');
    const todoList = ref([]);

    const onSubmit = (e) => {
      //console.log(todo.value);
      e.preventDefault();
      todoList.value.push({
          id: Date.now(),
          subject: todo.value
      });
    };

    return {
      todo, 
      onSubmit,
      todoList
    };
  }
}
</script>

<style>
.name {
  color: blue;
}
</style>
