<template>
  <div class="container">
    <!-- Form -->
    <form class="py-5 w-25 text-center" @submit.prevent="addTodoItem">
      <input class="form-control my-2" type="text" v-model="newTodoItem" />
      <input class="btn btn-primary" type="submit" value="Add Todo" />
    </form>

    <h1 class="row">Todo List</h1>
    <ul class="list-group list-group-flush">
      <li class="list-group-item list-item border-bottom rounded" v-for="todo in todos" :key="todo.id">
        <TodoItem :todoId="todo.id" :todoTitle="todo.title" :todo-completed="todo.completed" @delete-todo="(n) => deleteTodoItem(n)" />
      </li>
    </ul>
  </div>

</template>

<script>
import TodoItem from "@/components/TodoItem.vue";

let id = 0;
export default {
  name: "TodoList",
  components: {TodoItem},
  methods: {
    deleteTodoItem(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    addTodoItem() {
      this.todos.push({
        id: id++,
        title: this.newTodoItem,
        completed: false,
      });
      this.newTodoItem = "";
    },
  },
  data() {
    return {
      newTodoItem: "",
      todos: [
        {
          id: id++,
          title: "Todo One",
          completed: false,
        },
        {
          id: id++,
          title: "Todo Two",
          completed: true,
        },
        {
          id: id++,
          title: "Todo Three",
          completed: true,
        },
        {
          id: id++,
          title: "Todo Four",
          completed: false,
        },
        {
          id: id++,
          title: "Todo Four",
          completed: false,
        },
        {
          id: id++,
          title: "Todo Four",
          completed: false,
        },
        {
          id: id++,
          title: "Todo Four",
          completed: false,
        },
        {
          id: id++,
          title: "Todo Four",
          completed: false,
        }
      ],
    };
  }
}
</script>

<style>
.list-item {
  background-color: #181818;
}

</style>