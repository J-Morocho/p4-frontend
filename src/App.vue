<template>
  <div id="app">
      <router-view :user='credentials' :tokenLS='token' :LoggedIn='loggedIn' :url='URL' @loggedIn='logIn($event)'/>

  </div>
</template>

<script>

export default {
  name: 'App',
  data: function() {
    return {
      credentials: null,
      loggedIn: false,
      token: '',
      //URL: 'https://p4-backend1.herokuapp.com'
      URL: 'http://localhost:8000'
    }
  },
  methods: {
    logIn: function(event) {
      this.loggedIn = true
      // event consists of username, email, and token
      this.credentials = event
      // change the page
      this.$router.push('/home')
    },
    setToken: function() {
      this.token = localStorage.getItem('data')
    }
  },
  beforeMount: function () {
    this.setToken()
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
