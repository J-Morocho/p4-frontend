<template>
  <div id="app">
    <div class="container">
      <h1 class='title is-1'>Plantr</h1>
      <p>Username</p>
      <input class='input is-primary' type='text' v-model='username'/>
      <p>Password</p>
      <input class='input is-primary' type='password' v-model='password'/>
      <br>
      <button class='button'>Login</button>
      <br>
      <button class='button'>Sign Up</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: function() {
    return {
      username: "",
      password: "",
    }
  },
  methods: {
    // We need to grab the token and send it over to Home.vue
    handleLogin: function(){
      fetch('http://localhost:8000/api')
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
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: green;
}

.container {
  display: flex;
  flex-direction: column;
  padding: 2em;
}

p {
  text-align: left;
}

</style>
