<template>
  <div id="app">
      <router-view :url='url' @loggedIn='logIn($event)'/>

  </div>
</template>

<script>

export default {
  name: 'App',
  data: function() {
    return {
      loggedIn: false,
      tokens: {},
      url: 'http://localhost:8000'
    }
  },
  methods: {
    logIn: function(event) {
      this.loggedIn = true
      this.tokens = event
      // change the page
      this.$router.push({ path: 'home', query: { tokens: this.tokens, URL: this.URL }})
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
