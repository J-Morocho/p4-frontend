<template>
  <div id="Home">
    <div class="p-0" id="nav">
      <Header/>
    </div>
    <div class="media">
      <!-- Add listener to sidebar -->
      <Sidebar :user='credentials' :url='URL'/>
      <button class="button">New Plant</button>
      <div class='c'>
        <div class="card-container" v-for="plant in plants" v-bind:key="plant.id">
          <Card v-bind:name='plant.name' v-bind:description='plant.description'/>
        </div>
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
      category_id: null,
      plants: null,
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
      .then(data => {this.plants = data.results})
    },
    getPlantsInCategory: function(){
      fetch(`${this.URL}/api/categories/${this.category_id}/plants/`, {
        method: 'get',
        headers: {
          'Authorization': `JWT ${this.token}`
        }
      })
      .then(response => response.json())
      .then(data => {this.plants = data.results})
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

.c {
  display: flex;
  flex-wrap: wrap;
}

.content-container {
  padding: 20px;
  display: flex;
  flex-direction: column;
}
</style>