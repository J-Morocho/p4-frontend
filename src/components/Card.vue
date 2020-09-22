<template>
  <div class="card">
      <header class="card-header">
        <p class="card-header-title">{{name}}</p>
      </header>
      <div class="card-content">
          <div class="content">{{description}}</div>
          <div class="content"> Watered: {{is_watered}} </div>
          <div class="content" v-bind:next_watering='next_watering'> Next time: {{next_watering}}</div>
      </div>
      <footer class="card-footer">
          <a class="card-footer-item up" v-on:click='waterPlantHandler'>Water Plant</a>
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
            can_be_watered: true,
            freq: this.frequency,
            next_watering: '',

        }
    },
    methods: {
        dateDiff: function() {
            // This function returns the difference in milliseconds between the current time 
            // and the time the plant was last watered

            // When the plant was last watered at in milliseconds
            const t_0 = new Date(this.watered).getTime()
            // The current time in milliseconds
            const t_i = new Date()
        
            return t_i - t_0
        },
        getPlantTime: function() {
            let today = new Date()
            const m = today.getUTCMonth() + 1
            const d = today.getUTCFullYear()+ "-" + m + "-" + today.getUTCDate()
            const t = today.getUTCHours() + ":" + today.getUTCMinutes() + ":" + today.getUTCSeconds()
            return d+"T"+t
        },
        waterPlantHandler: function() {
                // The minimum amount of time that needs to elapse before the next watering
                console.log('watered', this.watered)
                let previous = new Date(this.watered).getTime()
                let t_0 = new Date()
                t_0.setTime(previous)
                let minWaitTime = (24/this.frequency) * 3600000
                this.next_watering = new Date(t_0.getTime() + minWaitTime)

                let d_t = this.dateDiff()
                //this.next_watering = new Date(n_t.getTime() + minWaitTime)
                if (!d_t < minWaitTime) {
                    // If plant needs watering then send patch request
                    const data = {category: this.category_id, name:this.name,
                    is_watered: "true", watered_at: this.getPlantTime() + "Z"}

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

                    this.$emit('watered')
                    this.$buefy.notification.open({
                        message: 'Watered Plant!',
                        type: 'is-info',
                        duration: 1000
                    })
                } else {
                    this.$emit('watered')
                    alert('You need to wait...')
                }
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