<template>
  <div class="todoList_list">
    <ul class="todoList_tab">
      <li>
        <a href="#" @click="filterStatus = 'all'" :class="{ active: filterStatus === 'all' }"
          >全部</a
        >
      </li>
      <li>
        <a
          href="#"
          @click="filterStatus = 'incomplete'"
          :class="{ active: filterStatus === 'incomplete' }"
          >待完成</a
        >
      </li>
      <li>
        <a
          href="#"
          @click="filterStatus = 'completed'"
          :class="{ active: filterStatus === 'completed' }"
          >已完成</a
        >
      </li>
    </ul>
    <div class="todoList_items">
      <ul class="todoList_item">
        <TodoItem
          v-for="todo in filterTodo"
          :key="todo.id"
          :todo="todo"
          @remove-todo="emit('remove-todo', $event)"
        />
      </ul>
      <div class="todoList_statistics">
        <p>{{ incompleteTodos.length }}個未完成項目</p>
      </div>
    </div>
  </div>
</template>
<script setup>
import TodoItem from './TodoItem.vue'
import { computed, ref } from 'vue'

const props = defineProps({
  todos: {
    type: Array,
    require: true,
  },
})
const emit = defineEmits(['remove-todo'])

const filterStatus = ref('all')
const filterTodo = computed(() => {
  if (filterStatus.value === 'incomplete') {
    return props.todos.filter((e) => e.status === false)
  } else if (filterStatus.value === 'completed') {
    return props.todos.filter((e) => e.status === true)
  } else {
    return props.todos
  }
})

const incompleteTodos = computed(() => {
  return props.todos.filter((e) => e.status === false)
})
</script>
