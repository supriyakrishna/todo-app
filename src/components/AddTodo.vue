<template>
  <div class="header">
    <h1>Todo List</h1>
    <form
      @submit.prevent="
        $emit('add-todo', title);
        title = '';
      "
    >
      <input type="text" v-model="title" placeholder="enter todo" />
      <input type="submit" value="Add Todo" class="addBtn btn" />
    </form>
    <button class="btn" @click="$emit('delete-all-todos')">
      Clear All Todos
    </button>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
    };
  },
};
</script>

<style scoped>
.header:after {
  content: "";
  display: table;
  clear: both;
}
input {
  margin: 0;
  border: none;
  border-radius: 0;
  width: 75%;
  padding: 10px;
  float: left;
  font-size: 16px;
}
.addBtn {
  width: 25%;
  float: left;
}
.addBtn:hover {
  background-color: #bbb;
}
button {
  float: right;
  margin: 10px 0px;
}
</style>
