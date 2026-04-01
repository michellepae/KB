<template>
  <div class="row mb-3">
    <div class="col">
      <div class="input-group">
        <input
          type="text"
          class="form-control"
          placeholder="할일을 여기에 입력!"
          v-model.trim="todo"
          @keyup.enter="addTodoHandler"
        />
        <span class="btn btn-primary input-group-addon" @click="addTodoHandler">추가</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// 이름 정의 (필요한 경우에만 작성, 보통 파일명이 이름이 됨)
// defineOptions({ name: 'InputTodo' }); 

// 반응형 데이터 선언 (data -> ref)
const todo = ref('');

//  Emit 정의 (emits 옵션 대용)
const emit = defineEmits(['add-todo']);

// 핸들러 함수 구현 (methods -> function)
const addTodoHandler = () => {
  if (todo.value.length >= 3) {
    // 부모에게 이벤트와 값 전달
    emit('add-todo', todo.value);
    // 입력창 초기화
    todo.value = ''; 
    return;
  }
  alert('할 일은 3글자 이상 입력해주세요.');
};
</script>
