<template>
<nav class="navbar p-3 mb-5 navbar-expand-lg navbar-light" style="background-color: #007bff; box-shadow: 0 0 10px rgba(0, 123, 255, 0.5);">
  <div class="container">
    <router-link to="/" class="navbar-brand mx-auto" style="color: #fff; text-shadow: 0 0 10px rgba(0, 123, 255, 0.8);">Home</router-link>
  </div>
  <!-- <div class="container">
    <router-link to="/upload" class="navbar-brand mx-auto" style="color: #fff; text-shadow: 0 0 10px rgba(0, 123, 255, 0.8);">Upload</router-link>
  </div> -->
</nav>
  <router-view/>
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
