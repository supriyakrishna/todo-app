<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" v-on:delete-all-todos="deleteAllTodos" />

    <Todos v-bind:todos="filteredTodos" v-on:del-todo="deleteTodo" />
    <button @click="filter = 'all'">All</button>
    <button @click="filter = 'complete'">Completed</button>
    <button @click="filter = 'active'">InComplete</button>
  </div>
</template>

<script>
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
export default {
  name: "App",
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "todo one",
          completed: true,
          editing: false
        },
        {
          id: 2,
          title: "todo two",
          completed: true,
          editing: false
        },
        {
          id: 3,
          title: "first",
          completed: false,
          editing: false
        }
      ],
      count: 0,
      filter: "all"
    };
  },
  methods: {
    addTodo(title) {
      this.count = this.todos.length + 1;
      this.todos.push({ id: this.count, title, completed: false });
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(item => item.id !== id);
    },
    deleteAllTodos() {
      this.todos = [];
    },
    sortAlphabetically(obj) {
      return obj.sort((a, b) => {
        if (a.title < b.title) return -1;
        if (a.title > b.title) return 1;
      });
    }
  },
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      } else if (this.filter === "active") {
        return this.todos.filter(item => item.completed === false);
      } else if (this.filter === "complete") {
        let temp = this.todos.filter(item => item.completed === true);
        return this.sortAlphabetically(temp);
        // return temp.sort(function(a, b) {
        //   if (a.title < b.title) {
        //     return -1;
        //   }
        //   if (a.title > b.title) {
        //     return 1;
        //   }
        // });
      }
      return this.todos;
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.header {
  background-color: black;
  padding: 30px 40px;
  color: white;
  text-align: center;
}
button {
  padding: 10px 20px 10px 20px;
  background: #d9d9d9;
  color: #555;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
  margin: 5px;
}
</style>
