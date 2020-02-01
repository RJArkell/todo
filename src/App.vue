<template>
  <md-app>
    <md-app-toolbar>
      <h1>Todo App</h1>
    </md-app-toolbar>
    <md-app-content>
      <md-subheader>
        <md-field>
          <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo"></md-input>
        </md-field>
      </md-subheader>
      <ul class="todos">
        <li v-for="todo in todos" :key="todo.id">
          <md-card>
            <input class="completeButton" type="checkbox" v-model="todo.completed" />
            <span
              v-if="todo.editing === false"
              class="todo-item-label"
              :class="{'is-complete': todo.completed}"
              @dblclick="editTodo(todo)"
            >{{ todo.label }}</span>
            <div v-if="todo.editing">
              <md-field>
                <md-input
                  type="text"
                  v-model="todo.label"
                  @keyup.enter="stopEdit(todo)"
                  @keyup.esc="stopEdit(todo)"
                  @focusout="stopEdit(todo)"
                ></md-input>
              </md-field>
            </div>
            <br />
            <button @click="removeTodo(todo)">
              <md-icon>delete</md-icon>
            </button>
            <button @click="editTodo(todo)">
              <md-icon>edit</md-icon>
            </button>
          </md-card>
        </li>
      </ul>
    </md-app-content>
  </md-app>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      editedTodo: ""
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        editing: false
      });
      this.currentTodo = "";
    },
    toggleCompleted() {
      this.todo.completed = !this.todo.completed;
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      todo.editing = true;
    },
    stopEdit(todo) {
      todo.editing = false;
    }
  }
};
</script>

<style>
ul {
  list-style-type: none;
  padding: 0px;
}
.md-app {
  max-width: 800px;
  margin: 30px auto;
  background: rgb(108, 188, 199);
}
.md-card {
  margin: 10px auto;
  background: lightgrey;
}
.md-checkbox {
  display: flex;
}
.md-app-toolbar {
  background: lightgrey;
}
.md-field {
  border-bottom: 2px dotted;
}
.is-complete {
  text-decoration: line-through;
}
</style>
