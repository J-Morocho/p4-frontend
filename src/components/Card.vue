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
    props: ['url', 'name', 'description', 'is_watered', 'p_id', 'watered', 'frequency'],
    data: function(){
        return {
            URL: this.url,
            category_id: localStorage.getItem('categoryId'),
            token: null,
            plant_id: this.p_id,
            watered_count: null,
            watered_at: this.watered,
            freq: this.frequency
        }
    },
    methods: {
        dateDiff: function(watered_at) {
            console.log(new Date(Date.now()) - new Date(watered_at))
        },
        waterPlantHandler: function() {
            let today = new Date()
            const m = today.getUTCMonth() + 1
            const d = today.getUTCFullYear()+ "-" + m + "-" + today.getUTCDate()
            const t = today.getUTCHours() + ":" + today.getUTCMinutes() + ":" + today.getUTCSeconds()

            // Get data watering data from plant
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
                    this.watered_at = data.watered_at
                    this.watered_count = data.watered_count
                    this.dateDiff(this.watered_at)
                    // Tells us how often (in minutes) we should water the plant
                    this.f = (24/data.frequency) * 60
                    console.log(this.f)
                    this.$emit('watered')
                    this.$buefy.notification.open({
                        message: 'Watered Plant!',
                        type: 'is-info',
                        duration: 1000
                    })

                }
            })
            
            const data = {category: this.category_id, name: this.name, is_watered: "true", watered_at: d+"T"+t+"Z" }
            console.log('plant watered at range', t - this.watered_at.slice(11, 19))

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
                    this.$buefy.notification.open({
                        message: 'Removed Plant',
                        type: 'is-danger',
                        duration: 600
                    })
                    this.$emit('removed')
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