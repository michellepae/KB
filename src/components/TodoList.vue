<template>
  <div class="row">
    <div class="col">
      <ul class="list-group" v-if="todoList.length > 0">
        <TodoListItem
          v-for="todoItem in todoList"
          :key="todoItem.id"
          :todoItem="todoItem"
          @delete-todo="$emit('delete-todo', $event)"
          @toggle-completed="$emit('toggle-completed', $event)"
        />
      </ul>

      <div v-else class="alert alert-info text-center">
        <h2>🎉 Completed! 🎉</h2>
        할 일이 없습니다. 할 일을 추가해주세요!
      </div>
    </div>
  </div>
</template>

<script setup>
import TodoListItem from './TodoListItem.vue';

//  Props 정의 (defineProps 사용)
const props = defineProps({
  todoList: {
    type: Array,
    required: true
  }
});

//  Emits 정의 (defineEmits 사용)
defineEmits(['delete-todo', 'toggle-completed']);
</script>
