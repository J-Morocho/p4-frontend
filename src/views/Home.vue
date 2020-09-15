<template>
  <div id="Home">
    <div class="p-0" id="nav">
      <Header v-bind:URL="URL"/>
    </div>
    <div class="media">
      <Sidebar/>
      
      <h1>HEY</h1>
    </div>
  </div>
</template>

<script>
import Header from '../components/Header'
import Sidebar from '../components/Sidebar'
// import Footer from './components/Footer'

export default {
  name: 'Home',
  components: {
    Header,
    Sidebar
  },
  // for components access
  data: function() {
    return {
      loggedIn: false,
      token: '',
      // Obtained from login page

      URL: 'http://localhost:8000'
    }
  }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}


#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>