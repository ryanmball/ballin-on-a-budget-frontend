<template>
  <div id="app">
    <div id="nav">
      <span v-if="isLoggedIn()">
        <router-link :to="`/users/${userID()}`">Dashboard</router-link>
        |
        <router-link to="/expenses">New Expense</router-link>
        |
        <router-link to="/incomes">New Income</router-link>
        |
        <router-link to="/balances">New Monthly Balance</router-link>
        |
        <router-link to="/logout">Logout</router-link>
      </span>
      <span v-else>
        <router-link to="/login">Login</router-link>
        |
        <router-link to="/signup">Signup</router-link>
      </span>
    </div>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      user: {},
    };
  },
  created: function () {
    axios.get(`/users/${localStorage.getItem("user_id")}`).then((response) => {
      console.log("Current User", response.data);
      this.user = response.data;
    });
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
    userID: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
