<template>
  <div id="Home">
    <div class="p-0" id="nav">
      <Header v-bind:URL="URL"/>
    </div>
    <div class="media">
      <Sidebar/>
      <button class="button">New Plant</button>
      <div class="content-container">
        <!-- Pass user data into this card -->
        <!-- This will need to be updated per category -->
        <Card/>
      </div>
    </div>
  </div>
</template>

<script>
import Header from '../components/Header'
import Sidebar from '../components/Sidebar'
// import Footer from './components/Footer'
import Card from '../components/Card'


export default {
  name: 'Home',
  components: {
    Header,
    Sidebar,
    Card,
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
  color: #ffffff;
}



.content-container {
  padding: 20px;
}
</style>