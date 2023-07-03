<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav>
    <header>
      <nav>
        <ul>
          <li><router-link to="/">Weather</router-link></li>
          <li><router-link to="/location">Location</router-link></li>
          <li><router-link to="/stopwatch">Stopwatch</router-link></li>
          <li><router-link to="/tictactoe">Tic Tac Toe</router-link></li>
          <li><router-link to="/photo">Photo</router-link></li>
        </ul>
      </nav>
    </header>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #42b983;
}
nav {
  padding: 30px;
}
header {
  background: #212;
  padding: 20px;
}
nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
nav li {
  display: inline-block;
  margin-right: 10px;
}
nav a {
  font-weight: bold;
  color: #2c3e;
  color: #e00b0b;
  text-decoration: none;
  padding: 5px 10px;
}
nav a.router-link-exact-active {
  color: #eff5f2;
}
nav a:hover {
  text-decoration: underline;
}
</style>
