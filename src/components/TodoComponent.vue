<template>
  <div class="container">
    <div v-bind:key="index" v-for="(todo, index) in todos">
      <TodoItem
        @completed-todo="$emit('completed-todo', { index: index })"
        @del-todo="$emit('del-todo', todo.id)"
        @edit-todo="$emit('edit-todo', { index: index })"
        v-bind:todo="todo"
        :valueindex="index"
      />
    </div>
  </div>
</template>
<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "TodoComponent",
  components: {
    TodoItem,
  },
  props: ["todos"],
};
</script>
