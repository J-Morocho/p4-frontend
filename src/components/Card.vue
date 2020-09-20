<template>
  <div class="card">
      <header class="card-header">
        <p class="card-header-title">{{name}}</p>
      </header>
      <div class="card-content">
          <div class="content">{{description}}</div>
          <div class="content"> Watered: {{is_watered}} </div>
      </div>
      <footer class="card-footer">
          <a class="card-footer-item up" v-on:click='waterPlantHandler'>Water Plant</a>
          <a class="card-footer-item up">Edit</a>
          <a class="card-footer-item del" v-on:click='deletePlantHandler'>Delete</a>
      </footer>
      
  </div>
</template>

<script>
export default {
    name: 'Card',
    props: ['url', 'name', 'description', 'is_watered', 'p_id'],
    data: function(){
        return {
            URL: this.url,
            category_id: localStorage.getItem('categoryId'),
            token: null,
            plant_id: this.p_id,
            watered_count: null,
            watered_at: null
        }
    },
    methods: {
        waterPlantHandler: function() {
            let today = new Date()
            const m = today.getUTCMonth() + 1
            const d = today.getUTCFullYear()+ "-" + m + "-" + today.getUTCDate()
            const t = today.getUTCHours() + ":" + today.getUTCMinutes() + ":" + today.getUTCSeconds()+"Z"

            fetch(`${this.URL}/api/plants/${this.plant_id}/`, {
                method: 'get',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `JWT ${this.token}`
                }
            })
            .then(response => {
                if (!response.ok) {
                    response.json()
                } else {
                    return response.json()
                }
            })
            .then(data => {
                if (data) {
                    console.log('d', data)
                    this.watered_at = data.watered_at
                    this.watered_count = data.watered_count
                    this.f = data.frequency
                }
            })
            
            const data = {category: this.category_id, name: this.name, is_watered: "true", watered_at: d+"T"+t }
            fetch(`${this.URL}/api/plants/${this.plant_id}/`, {
                method: 'patch',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `JWT ${this.token}`
                },
                body: JSON.stringify(data)
                
            })
            .then(response => {
                if (!response.ok){
                    console.log(response)
                    response.json()
                } else {
                    return response.json()
                }
            })
            .then(data => {
                if (data) {
                    console.log(data)
                } else {
                    alert('something went wrong')
                }
            })
        },
        deletePlantHandler: function() {
            fetch(`${this.URL}/api/plants/${this.plant_id}/`, {
                method: 'delete',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `JWT ${this.token}`
                }
            })
            .then(response => {
                if (response.json()) {
                    alert('plant removed')
                }
            })
        }
    },
    beforeMount: function () {
        this.token = localStorage.getItem('data')
    }
}
</script>

<style>
.card-header-title {
    font-size: 10px;
}

.del {
    color: red;
}

.up {
    color: #26537e;
}



</style>