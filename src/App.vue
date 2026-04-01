<script setup>
import { ref } from 'vue';
import TodoList from './components/TodoList.vue';
import InputTodo from './components/InputTodo.vue';

// 1. 상태 관리 (data -> ref)
const ts = new Date().getTime();
const todoList = ref([
  { id: ts, todo: '자전거 타기', completed: false },
  { id: ts + 1, todo: '딸과 공원 산책', completed: true },
  { id: ts + 2, todo: '일요일 애견 카페', completed: false },
  { id: ts + 3, todo: 'Vue 원고 집필', completed: false },
]);

// 2. 기능 구현 (methods -> functions)
const addTodo = (todo) => {
  if (todo.length >= 2) {
    todoList.value.push({
      id: new Date().getTime(),
      todo: todo,
      completed: false,
    });
  }
};

const deleteTodo = (id) => {
  const index = todoList.value.findIndex((item) => item.id === id);
  if (index !== -1) {
    todoList.value.splice(index, 1);
  }
};

const toggleCompleted = (id) => {
  const index = todoList.value.findIndex((item) => item.id === id);
  if (index !== -1) {
    todoList.value[index].completed = !todoList.value[index].completed;
  }
};

const clearAll = () => {
  if (confirm("정말 모든 할 일을 삭제하시겠습니까?")) {
    todoList.value = [];
  }
};
</script>

<template>
  <div id="app" class="container">
    <div class="card card-body bg-light py-2">
      <div class="title">
        :: Todolist App
        <span class="float-end badge bg-danger pointer" @click="clearAll">전체 삭제</span>
      </div>
    </div>
    
    <div class="card card-default card-borderless">
      <div class="card-body">
        <InputTodo @add-todo="addTodo" />
        <br />
        <div class="list-group">
          <TodoList
            :todoList="todoList"
            @toggle-completed="toggleCompleted"
            @delete-todo="deleteTodo"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.pointer { cursor: pointer; }
</style>