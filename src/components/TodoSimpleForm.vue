<template>
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
</template>

<script>
import {ref} from 'vue';

export default {
    emits: ['add-todo'], // 부모로 보내는 이벤트
    setup(props, { emit }) {
        const todo = ref('');
        const hasError = ref(false);
        const onSubmit = (e) => {
            e.preventDefault();
            if (todo.value === '') {
                hasError.value = true;
            } else {
                // 자식 컴포넌트에서 부모 컴포넌트로 보냄
                emit('add-todo', {
                    id: Date.now(),
                    subject: todo.value,
                    completed: false
                }); 
                hasError.value = false;
                todo.value = ''; // 입력창 clear
            }
        };

        return {
            todo, hasError, onSubmit
        }
    }
}
</script>

<style>

</style>
