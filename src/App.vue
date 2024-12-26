<template>
  <h1>Список запланированных дел</h1>

  <Todo v-for="todo in todos" :key="todo.id" :id="todo.id" :point="todo.point" @remove="remove" @change="change" />

  <TodoForm 
  @add="add" 
  />
</template>

<script>
import Todo from "../src/components/Todo.vue";
import TodoForm from "../src/components/TodoForm.vue";

export default {
  components: {
    Todo,
    TodoForm,
  },
  data() {
    return {
      todos: [
        { id: 1, point: "Проснуться" },
        { id: 2, point: "Умыться" },
        { id: 3, point: "Почистить зубы" },
      ],
    };
  },
  methods: {
    remove(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    change(id, point) {
      const index = this.todos.findIndex((todo) => todo.id === id);
      if (index !== -1) {
        this.todos[index].point = point;
      }
    },
    add(point) {
      let id = this.todos.length + 1;
      this.todos.push({
        id,
        point
      })
    },
  }
};
</script>


<style scoped>



</style>