<template>
  <div id="Home">
    <div class="p-0" id="nav">
      <Header :user='credentials' :url='URL'/>
    </div>
    <div class="media">
      <show-at :breakpoints="{medium: 1365, large: 1365}" breakpoint="medium">
        <Sidebar :user='credentials' :url='URL' @category_id='getPlantsInCategory($event)'/>
      </show-at>
      <div class="content">
        <ModalCreatePlant :user='credentials' 
                          :url='URL' 
                          :cat_ids='category_id' 
                          @add_plant_event='getPlantsInCategory'/>
        <div v-if='no_data'> No data to show </div>
        <div class='c'>
          <div class="card-container" v-for="plant in plants" v-bind:key="plant.id">
            <Card v-bind:name='plant.name' 
                  v-bind:description='plant.description'
                  v-bind:is_watered="plant.is_watered"
                  :watered="plant.updated_at"
                  v-bind:frequency="plant.frequency"
                  :p_id="plant.id"
                  :url="URL"
                  @removed='getPlantsInCategory'
                  @watered='getPlantsInCategory'
                  />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from '../components/Header'
import Sidebar from '../components/Sidebar'
import ModalCreatePlant from '../components/ModalCreatePlant'
import Card from '../components/Card'
import {showAt} from 'vue-breakpoints'

export default {
  name: 'Home',
  props: ['url', 'LoggedIn', 'user', 'tokenLS'],
  components: {
    Header,
    Sidebar,
    Card,
    showAt,
    ModalCreatePlant,
  },
  // for components access
  data: function() {
    return {
      categories: [],
      // Default no category selected
      category_id: null,
      plants: null,
      no_data: false,
      // TODO: Change login based on App.vue Login value
      loggedIn: this.LoggedIn,
      credentials: this.user,
      token: '',
      URL: this.url
    }
  },
  methods: {
    displayCategories: function() {
      fetch(`${this.URL}/api/categories/`, {
          method: 'GET',
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
      .then(data => {
          this.plants = data.results
          if (!this.plants) {
            console.log('empty')
          }
        })
    },
    getPlantsInCategory: function(){
      // Set category_id of category that is currently clicked
      this.category_id = localStorage.getItem('categoryId')

      fetch(`${this.URL}/api/categories/${this.category_id}/plants`, {
        method: 'GET',
        headers: {
          'Authorization': `JWT ${this.token}`
        }
      })
      .then(response => response.json())
      .then(data => {
          this.plants = data.results
          if (this.plants == 0) {
            this.no_data = true
          } else {
            this.no_data = false
          }
        })
    },
  },
  beforeMount: function() {
    this.token = localStorage.getItem('data')
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

.content {
  padding: 20px;
  width: 100%;
}
.content-container {
  padding: 20px;
  display: flex;
  flex-direction: column;
}

.card-container {
  margin: 10px;
  width: 460px;
}


</style>