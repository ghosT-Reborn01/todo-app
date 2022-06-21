<template>
  <div>
    <form @submit="addTodo">
      <input
        type="text"
        v-model="title"
        name="title"
        placeholder="Add TODO"
        class="input__field"
      />
    </form>
    <div v-if="temp_todo == null">
      <button class="btn" v-on:click="addTodo">Add Todo</button>
    </div>
    <div v-else>
      <button class="btn btn--update" v-on:click="updateTodo">Update</button>
      <button class="btn btn--cancel" v-on:click="updateCancel">Cancel</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "AddTodo",
  props: ["temp_todo"],
  data() {
    return {
      title: "",
    };
  },
  watch: {
    temp_todo() {
      if (this.temp_todo != null) {
        this.title = this.temp_todo.title;
        //   alert("updated");
        // } else {
        //   alert("not updaetd");
      }
    },
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        id: Math.floor(Math.random() * 100),
        title: this.title,
        completed: false,
      };
      this.$emit("add-todo", newTodo);
      this.title = "";
    },
    updateTodo() {
      // console.log(this.title);
      this.$emit("update-todo", this.title);
      setTimeout(() => {
        this.title = "";
      }, 1000);
    },
    updateCancel() {
      this.$emit("update-cancel", this.title);
      this.title = ""
    },
  },
};
</script>

<style scoped>
* {
  background-color: rgba(240, 248, 255, 0.373);
  margin: 5px;
}
.btn {
  padding: 10px;
  border: none;
  cursor: pointer;
  border: 1px dotted rgba(128, 128, 128, 0.493);
  border-radius: 10px;
}
.input__field {
  text-align: center;
  margin: auto;
  padding: 10px;
  width: 50%;
  border: 1px dotted rgba(128, 128, 128, 0.493);
  border-radius: 10px;
}
.btn--update {
  background-color: rgba(0, 128, 0, 0.278);
}
.btn--cancel {
    background-color: rgba(255, 0, 0, 0.35);
}
</style>
