<template>
  <li
    class="list-group-item"
    :class="{ 'list-group-item-success': todoItem.completed }"
    @click="$emit('toggle-completed', todoItem.id)"
  >
    <input 
      type="checkbox" 
      class="pointer me-3" 
      :checked="todoItem.completed"
      @click.stop="$emit('toggle-completed', todoItem.id)"
    />
    
    <span class="pointer" :class="{ 'todo-done': todoItem.completed }">
      {{ todoItem.todo }}
      {{ todoItem.completed ? '(완료)' : '' }}
    </span>

    <span
      class="float-end badge bg-secondary pointer"
      @click.stop="$emit('delete-todo', todoItem.id)"
    >삭제</span>
  </li>
</template>

<script setup>
// Props 정의
const props = defineProps({
  todoItem: { 
    type: Object, 
    required: true 
  }
});

// Emits 정의
defineEmits(['toggle-completed', 'delete-todo']);
</script>

<style scoped>
.pointer { cursor: pointer; }
.todo-done { text-decoration: line-through; }
</style>
