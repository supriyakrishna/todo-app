<template>
  <div>
    <ul>
      <li v-for="todo in todos" v-bind:key="todo.id">
        <div
          v-if="!todo.editing"
          @dblclick="editTodo(todo)"
          v-bind:class="{ completed: todo.completed }"
        >
          <input type="checkbox" @change="toggleCompleted(todo)" />
          <label>{{ todo.title }}</label>
          <span class="close" @click="$emit('del-todo', todo.id)">×</span>
        </div>
        <input
          v-focus
          v-else
          type="text"
          v-model="todo.title"
          @blur="completeEdit(todo)"
          @keyup.enter="completeEdit(todo)"
        />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Todos",
  props: ["todos"],
  data() {
    return {};
  },
  directives: {
    focus: {
      // directive definition
      inserted: function(el) {
        el.focus();
      },
    },
  },
  methods: {
    editTodo(todo) {
      todo.editing = true;
    },
    completeEdit(todo) {
      todo.editing = false;
    },
    toggleCompleted(todo) {
      todo.completed = !todo.completed;
    },
  },
};
</script>

<style scoped>
ul {
  margin: 0;
  padding: 0;
}
ul li {
  cursor: pointer;
  position: relative;
  padding: 12px 8px 12px 40px;
  list-style-type: none;
  background: lightgrey;
  font-size: 18px;
  transition: 0.2s;
}
.close {
  position: absolute;
  right: 0;
  top: 0;
  padding: 12px 16px 12px 16px;
}
.close:hover {
  background-color: red;
  color: white;
}
ul li {
  text-align: left;
}
.completed {
  text-decoration-line: line-through;
}
</style>
