<template>
  <div class="todo__data" v-bind:class="{ 'is-complete': todo.completed }">
    <input class="complete__box" type="checkbox" v-on:click="markList" />
    <p class="text__align">{{ todo.title }}</p>
    <button v-on:click="editList" class="btn btn--edit">Edit</button>
    <br />
    <button v-on:click="deleteList" class="btn btn--delete">Delete</button>
  </div>
</template>
<script>
export default {
  name: "TodoItem",
  props: ["todo", "valueindex"],
  methods: {
    markList() {
      this.$emit("completed-todo", this.todo);
    },
    deleteList() {
      this.$emit("del-todo", this.todo.id);
    },
    editList() {
      this.$emit("edit-todo", this.todo);
    },
  },
};
</script>

<style scoped>
.is-complete {
  text-decoration: line-through;
  color: rgba(0, 0, 0, 0.453);
}
.todo__data {
  text-align: center;
  display: flex;
  align-items: center;
  border-bottom: 1px rgba(189, 189, 189, 0.512) solid;
  padding-bottom: 5px;
  background-color: aliceblue;
  padding: 20px;
  margin: auto;
}
.text__align {
  margin: auto;
}
.btn {
  padding: 8px;
  background-color: aliceblue;
  border-radius: 10px;
  cursor: pointer;
  border: 1px solid gray;
  margin: 3px;
  border: none;
}
.complete__box {
  height: 30px;
  width: 30px;
}
.btn--edit {
  background-color: rgba(0, 128, 0, 0.521);
}
.btn--delete {
  background-color: rgba(255, 0, 0, 0.5);
}
</style>
