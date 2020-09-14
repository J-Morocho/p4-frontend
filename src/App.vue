<template>
  <div id="app">
      <router-view/>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: function() {
    return {
      username: "",
      password: "",
      loggedIn: false,
    }
  },
  methods: {
    // We need to grab the token and send it over to Home.vue
    handleLogin: function(){
      fetch('http://localhost:8000/auth/users/login/')
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.container {
  display: flex;
  flex-direction: column;
  padding: 2em;
}

label {
  text-align: left;
}

.button {
  background-color: #2D669B;
}
</style>
