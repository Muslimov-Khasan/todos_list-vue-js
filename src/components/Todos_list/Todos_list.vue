<template>
  <div class="continer">
    <h1 class="text">Todo App</h1>
    <form class="form" @submit.prevent="addTodo">
      <input
        class="input form-control w-25"
        v-model="newTodo"
        placeholder="Add a new todo"
      />
      <button class="btn btn-dark">Add</button>
    </form>
    <ul class="todo__list">
      <li class="item" v-for="(todo, index) in todos" :key="index">
        <strong v-if="editingIndex !== index">{{ todo }}</strong>
        <input class="edit w-25" v-else v-model="todos[index]" />
        <button class="button btn btn-success" @click="editingIndex = null">
          Save
        </button>
        <button class="button btn btn-info" @click="editTodo(index)">
          Edit
        </button>
        <button class="button btn btn-danger" @click="deleteTodo(index)">
          Delete
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: "",
      editingIndex: null,
    };
  },
  mounted() {
    const savedTodos = localStorage.getItem("todos");
    if (savedTodos) {
      this.todos = JSON.parse(savedTodos);
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== "") {
        this.todos.push(this.newTodo);
        this.newTodo = "";
        localStorage.setItem("todos", JSON.stringify(this.todos));
      }
    },
    editTodo(index) {
      this.editingIndex = index;
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style scoped>
.continer {
  margin-top: 200px;
}

.form {
  display: flex;
  margin: 0 auto;
  margin-left: 690px;
  margin-bottom: 30px;
}

.todo__list {
  text-align: center;
  list-style-type: none;
}

.text {
  text-align: center;
  margin-top: 20px;
}

.item {
  margin-bottom: 11px;
}

.button {
  margin-left: 11px;
}

.edit {
  border-radius: 30px;
  border: solid 2px red;
  outline: none;
}
</style>