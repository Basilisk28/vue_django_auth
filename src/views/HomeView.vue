<template>
  <div class="home">
    <h1>You've successfully logged in and this is the home page</h1>
    <div class="col-md-6 mx-auto">
      <div class="form-group d-flex">
        <input
          class="form-control"
          v-model="todo"
          placeholder="Enter Todo"
          type="text"
        />
        <button class="btn btn-success" @click="createTodo()">Create</button>
      </div>
      <ul class="list-group mt-4">
        <li class="list-group-item" v-for="todo in todos" :key="todo.uid">
          <strike v-if="todo.is_completed">
            {{ todo.todo_name }}
          </strike>
          <p v-else>{{ todo.todo_name }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "HomeView",
  components: {},

  data() {
    return {
      todo: "",
      todos: [],
    };
  },
  created() {
    this.getTodos();
  },
  methods: {
    getTodos() {
      const token = localStorage.getItem("token");
      const requestOptions = {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${token}`,
          // "Access-Control-Allow-Origin": "*",
        },
      };
      fetch("http://localhost:8000/api/todo/", requestOptions)
        .then((result) => result.json())
        .then((data) => {
          console.log(data.data.todo_name);
          this.todos = data.data;
          console.log(this.todos);
          // if (data.access !== undefined) {
          //   localStorage.setItem("token", data.access);
          // } else {
          //   // Display an alert for undefined credentials
          //   alert("Invalid login credentials");
          //   window.location.href = "/login";
          // }
          // window.location.href = "/";
        });
    },
    createTodo() {
      this.getTodos();
      const token = localStorage.getItem("token");
      console.log(token);
      const requestOptions = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: `Bearer ${token}`,
          // "Access-Control-Allow-Origin": "*",
        },
        body: JSON.stringify({
          todo_name: this.todo,
        }),
      };
      fetch("http://localhost:8000/api/todo/", requestOptions)
        .then((result) => result.json())
        .then((data) => {
          console.log(data.data.todo_name);
          // if (data.access !== undefined) {
          //   localStorage.setItem("token", data.access);
          // } else {
          //   // Display an alert for undefined credentials
          //   alert("Invalid login credentials");
          //   window.location.href = "/login";
          // }
          // window.location.href = "/";
        });
    },
  },
};
</script>
