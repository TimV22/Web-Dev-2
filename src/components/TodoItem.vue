<template>
  <div class="container" :id="todoId">
    <div class="row flex-wrap">
    <input class=" form-check-inline" type="checkbox" v-model="completed"/>
    <p class="px-3 h5" :class="{line: completed}">{{title}}</p>
    <button class="btn btn-sm btn-outline-danger list-item align-self-center" @click="$emit('delete-todo', id)">X</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todoTitle: {
      type: String,
      required: true,
    },
    todoId: {
      type: Number,
      required: true,
    },
    todoCompleted: {
      type: Boolean,
      required: true,
    }
  },
  data(){
    return {
      title: this.todoTitle,
      id: this.todoId,
      completed: this.todoCompleted,
    }
  }
}
</script>

<style scoped>

.line {
  text-decoration: line-through;
}
</style>