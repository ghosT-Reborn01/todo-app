<template>
  <AddTodo
    @add-todo="addTodo"
    @update-todo="updateText"
    @update-cancel="updateCancel"
    :temp_todo="temp_todo"
  />
  <TodoComponent
    :todos="todos"
    :key="todos.id"
    @completed-todo="markComplete"
    @del-todo="deletetodo"
    @edit-todo="editItem"
  />
</template>

<script>
import TodoComponent from "./components/TodoComponent.vue";
import AddTodo from "./components/AddTodo.vue";

export default {
  name: "App",
  components: {
    TodoComponent,
    AddTodo,
  },
  data() {
    return {
      temp_todo: null,
      selectedIndex: 0,
      todos: [
        {
          id: 1,
          title: "First Todo",
          completed: false,
        },
        {
          id: 2,
          title: "Second Todo",
          completed: false,
        },
        {
          id: 3,
          title: "Third Todo",
          completed: false,
        },
      ],
    };
  },
  methods: {
    markComplete(item) {
      // console.log(item);
      this.todos[item.index].completed = !this.todos[item.index].completed;
    },
    deletetodo(id) {
      // console.log(id);
      this.todos = this.todos.filter((todo) => todo.id != id);
    },
    editItem(id) {
      console.log(id);
      // console.log(this.temp_todo)
      this.temp_todo = this.todos[id.index];
      this.selectedIndex = id.index;
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    },
    updateText(update) {
      // console.log(update);
      this.todos[this.selectedIndex].title = update;
      this.temp_todo = null;
    },
    updateCancel(){
      this.temp_todo = null;
    }
  },
};
</script>

<style>
#app {
  text-align: center;
}
</style>
