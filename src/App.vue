<script>
export default {
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
<template>
  <nav>
    <router-link to="/">Home</router-link>
    |
    <router-link to="/about">About</router-link>
    |
    <router-link to="/movies">All movies</router-link>
    |
    <router-link to="/movies/new">Add movie</router-link>
    |
    <span v-if="isLoggedIn()">
      <router-link to="/movies/logout">Log out</router-link>
    </span>
    <span v-else>
      <router-link to="/movies/signup">Sign up</router-link>
      |
      <router-link to="/movies/login">Log in</router-link>
    </span>
  </nav>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
