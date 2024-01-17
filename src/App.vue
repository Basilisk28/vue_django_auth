<template>
  <div>
    <nav>
      <div class="navbar">
        <router-link v-if="isLoggedIn" to="/" class="nav-link"
          >Home</router-link
        >
        <router-link v-if="isLoggedIn" to="/about" class="nav-link"
          >About</router-link
        >
        <div v-if="!isLoggedIn" class="login-message">
          <h1>In order to access this app, you first need to login!</h1>
          <p>Use username: devanshu, pass: 123</p>
          <router-link to="/login" class="btn btn-primary">Login</router-link>
        </div>
        <button v-if="isLoggedIn" class="btn btn-danger" @click="logout">
          Logout
        </button>
      </div>
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoggedIn: false,
    };
  },
  created() {
    if (localStorage.getItem("token")) {
      this.isLoggedIn = true;
    }
  },
  methods: {
    logout() {
      localStorage.removeItem("token");
      window.location.href = "/login";
    },
  },
};
</script>

<style>
.navbar {
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: #3498db;
  color: #ffffff;
}

.nav-link {
  font-weight: bold;
  color: #ffffff;
  margin-right: 20px;
  text-decoration: none;
}

.login-message {
  text-align: center;
  margin-top: 20px;
}

.btn {
  display: inline-block;
  font-weight: bold;
  margin-top: 10px;
  margin-left: 20px;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  background-color: #2ecc71;
  color: #ffffff;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn:hover {
  background-color: #27ae60;
}

/* Styles for the "about" page */
.about {
  padding-top: 50px;
  text-align: center;
  font-size: 24px;
  color: #333;
}
</style>
