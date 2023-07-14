<template>
<!-- 줄여쓰기 v-bind: = :class -->
<!-- 줄여쓰기 v-on:   = @      -->
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
    <div class="card mt-2">
      <div class="card-body p-2">
          {{ todoList[0].subject }}
      </div>
    </div>
    <div class="card mt-2">
      <div class="card-body p-2">
        {{ todoList[1].subject }}
      </div>
    </div>
    
</div>

</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const todo = ref('');
    const todoList = ref([
      {id: 1, subject: '휴대폰 사기'},
      {id:2, subject: '장보기'}
    ]);

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
