<template>
  <div id="todoListPage" class="bg-half">
    <nav>
      <h1><a href="#">ONLINE TODO LIST</a></h1>
      <ul>
        <li class="todo_sm">
          <a href="#"><span>王小明的代辦</span></a>
        </li>
        <li><RouterLink to="/">登出</RouterLink></li>
      </ul>
    </nav>
    <div class="conatiner todoListPage vhContainer">
      <div class="todoList_Content">
        <TodoFrom @add-todo="addTodo" />
        <TodoList v-if="todos.length" :todos="todos" @remove-todo="removeTodo" />
        <p v-else>尚無待辦事項</p>
      </div>
    </div>
  </div>
</template>
<script setup>
import TodoFrom from '@/components/TodoFrom.vue'
import TodoList from '@/components/TodoList.vue'
import { ref } from 'vue'
import { RouterLink } from 'vue-router'

const todos = ref([
  { id: 1, content: '把冰箱發霉的檸檬拿去丟', status: false },
  { id: 2, content: '打電話叫媽媽匯款給我', status: true },
  { id: 3, content: '整理電腦資料夾', status: false },
  { id: 4, content: '繳電費水費瓦斯費', status: true },
  { id: 5, content: '約vicky禮拜三泡溫泉', status: false },
  { id: 6, content: '約ada禮拜四吃晚餐', status: true },
])

const addTodo = (content) => {
  if (content.trim() !== '') {
    todos.value.push({
      id: Date.now,
      content: content.trim(),
      status: false,
    })
  }
}

const removeTodo = (id) => {
  todos.value = todos.value.filter((e) => e.id !== id)
}
</script>
