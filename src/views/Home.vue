<template>
  <div id="Home">
    <div class="media">
      <Sidebar/>
      
      <!-- <Footer/> -->
    </div>
  </div>
</template>

<script>
import Sidebar from '../components/Sidebar'
// import Footer from './components/Footer'

export default {
  name: 'Home',
  components: {
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