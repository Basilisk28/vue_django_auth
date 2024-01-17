<template>
  <div class="about">
    <h1>This is a login page</h1>
    <div class="col-6 mx-auto">
      <form>
        <div class="mb-3" style="padding-bottom: 15px">
          <label for="exampleInputEmail1" class="form-label">Username </label>
          <input
            type="text"
            v-model="username"
            class="form-control"
            id="exampleInputEmail1"
            aria-describedby="emailHelp"
          />
        </div>
        <!-- {{ username }} -->
        <div class="mb-3">
          <label for="exampleInputPassword1" class="form-label"
            >Password
          </label>
          <input
            type="password"
            v-model="password"
            class="form-control"
            id="exampleInputPassword1"
          />
        </div>
        <button type="submit" @click="submit" class="btn btn-primary">
          Submit
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    submit(e) {
      // console.log(this.username);
      // console.log(this.password);
      e.preventDefault();

      if (!this.username.length) {
        alert("Fill Username");
      }

      if (!this.password.length) {
        alert("Fill password");
      }

      const requestOptions = {
        method: "POST",
        headers: {
          "Content-type": "application/json",
          // "Access-Control-Allow-Origin": "*",
        },
        body: JSON.stringify({
          username: this.username,
          password: this.password,
        }),
      };
      fetch("http://localhost:8000/api/token/", requestOptions)
        .then((result) => result.json())
        .then((data) => {
          // console.log(data.access);
          if (data.access !== undefined) {
            localStorage.setItem("token", data.access);
          } else {
            // Display an alert for undefined credentials
            alert("Invalid login credentials");
            window.location.href = "/login";
          }
          window.location.href = "/";
        });
    },
  },
};
</script>
