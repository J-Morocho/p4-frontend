<template>
  <div id="Home">
    <div class="p-0" id="nav">
      <Header/>
    </div>
    <div class="media">
      <Sidebar :user='credentials' :url='URL'/>
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
  props: ['url', 'LoggedIn', 'user'],
  components: {
    Header,
    Sidebar,
    Card,
  },
  // for components access
  data: function() {
    return {
      categories: [],
      // TODO: Change login based on App.vue Login value
      loggedIn: this.LoggedIn,
      credentials: this.user,
      token: this.user.token,
      URL: this.url
    }
  },
  methods: {
    displayCategories: function() {
      fetch(`${this.URL}/api/categories/`, {
          method: 'get',
          headers: {
              'Authorization': `JWT ${this.token}`
              }
          })
          .then(response => response.json())
          .then(data => this.categories = data.results)
    },
    getAllPlants: function() {
      fetch(`${this.URL}/api/plants/`, {
          method: 'get',
          headers: {
            'Authorization': `JWT ${this.token}`
          }
      })
      .then(response=> response.json())
      .then(data => console.log(data))
    },
    clearContainer: function(){ 
      return null
    },
  },
  before: function() {
    const {tokens, URL} = this.$route.query
    console.log(tokens, URL)
  },
  beforeMount: function() {
    this.displayCategories()
    this.getAllPlants()
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