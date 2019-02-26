<template>
  <div class="todo-list">
    <button @click="deleteAllTodo">할일 전체 삭제</button>
    <button @click="deleteAllCompletedTodo">완료된 할일 전체 삭제</button>
    <h2>Todos</h2>
    <ul>
      <li v-for="todo in todos" :key="todo.id" :class="{ completed: todo.completed }">
        <input type="checkbox" v-model="todo.completed" @change="completeTodo(todo)">
        {{ todo.title }}
        <button type="button" @click="deleteTodo(todo.id)">삭제</button>
      </li>
    </ul>
    <h2>Completed Todos</h2>
    <ul>
      <li v-for="todo in completedTodos" :key="todo.id">
        {{ todo.title }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  props: ['todos', "completedTodos", "deleteTodo", "deleteAllTodo", "deleteAllCompletedTodo", "completeTodo"]
}
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
