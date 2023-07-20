<template>
  <div v-for="(todo, index) in todoList" :key="todo.id">
      <div class="card mt-2">
        <div class="card-body p-2 d-flex aline-items-center">
          <!-- 목록 -->
          <div class="form-chekck flex-grow-1">
            <input class="form-cheeck-input" type="checkbox" :value="todo.completed" @change="toggleTodo(index)"/>
            <label class="form-check-label" :class="{ todo: todo.completed }">{{ todo.subject }}</label>
          </div>
          <!-- 삭제 -->
          <div>
            <button class="btn btn-danger btn-sm" @click="deleteTodo(index)">Delete</button>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
    props: ['todoList'], // 부모 컴포넌트에서 받음
    emits: ['toggle-todo', 'delete-todo'],

    setup(props, { emit }) {
        const toggleTodo = (index) => {
            emit('toggle-todo', index);
        };

        const deleteTodo = (index) => {
            emit('delete-todo', index);
        };

        return {
            toggleTodo,
            deleteTodo
        }
    }
}
</script>

<style>

</style>