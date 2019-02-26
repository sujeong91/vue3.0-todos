<template>
  <div class="todos">
    <form @submit.prevent="createTodo">
      <input type="text" placeholder="할일을 등록하세요."  v-model="todo.title">
    </form>
    <TodoList 
      :todos="todos"
      :completedTodos="completedTodos"
      :deleteTodo="deleteTodo"
      :deleteAllTodo="deleteAllTodo"
      :deleteAllCompletedTodo="deleteAllCompletedTodo"
      :completeTodo="completeTodo"
    >
    </TodoList>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'

export default {
  name: "Todos",
  components: { TodoList },
  data: function() {
    return {
      id : 0,
      todos: [],
      completedTodos: [],
      todo: {
        id: 0, 
        title: "",
        completed: false
      }
    };
  },
  methods : {
    createTodo () {
      this.id++

      const todo = {
        ...this.todo,
        id: this.id
      }

      this.todos = this.todos.concat(todo);

      this.todo.title = "";
    },
    deleteTodo (todoId) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== todoId && todo;
      });
    },
    deleteAllTodo () {
      this.todos = [];
    },
    deleteAllCompletedTodo() {
      this.completedTodos = []
      // console.log("1"+ this.completedTodos);
      // this.completedTodos = this.todos.filter(todo => {
      //   return todo.completed && todo;
      // });
      // console.log("2" + this.completedTodos);
    },
    completeTodo(completeTodo) {

      this.todos = this.todos.filter(todo => todo.id !== completeTodo.id && todo)

      this.completedTodos = this.completedTodos.concat(completeTodo)
    }
  }
}
</script>