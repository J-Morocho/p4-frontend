<template>
    <form action="">
            <div class="modal-card" style="width: auto">
                <header class="modal-card-head">
                    <p class="modal-card-title">Add Plant</p>
                </header>
                <section class="modal-card-body">
                    <b-field label="Plant Information">
                        <b-input type="text" v-model='plant_name' required></b-input>
                    </b-field>
                    <b-field label="Description">
                        <b-input maxlength="100" type="textarea" v-model='description' required></b-input>
                    </b-field>
                    <b-field label="Watering Frequency">
                        <b-input v-model.number='frequency'></b-input>
                        <p>Times per day</p>
                    </b-field>
                </section>

                <footer class="modal-card-foot">
                    <button class="button" type="button"  @click="$emit('close')">Close</button>
                    <button class="button is-primary" v-on:click="createPlant">Add</button>
                </footer>
            </div>
        </form>
</template>

<script>
export default {
    name: 'ModalFormPlant',
    props: ['cat_id', 'canCancel', 'url', 'user'],
    data: function() {
        return {
            plant_name: '',
            frequency: '',
            description: '',
            // Set to use local storage
            category_id: this.cat_id,
            credentials: this.user,
            token: '',
            URL: this.url,
        }
    },
    methods: {
        createPlant: function() {
            this.category_id = localStorage.getItem('categoryId')

            const data = {name: this.plant_name, category: this.category_id,
                        description: this.description}

            fetch(`${this.URL}/api/plants/`, {
              method: 'post',
              headers: {
                  'Content-Type': 'application/json',
                  'Authorization': `JWT ${this.token}`
              },
              body: JSON.stringify(data)
            })
            .then(response => {
                if (!response.ok) {
                    return response.json()
                } else {
                    response.json()
                }
            })
            .then(data => {
                if (data) {
                    this.$emit('add_plant_event', data)
                    this.$emit('close')
                }
            })

        }
    },
    beforeMount: function() {
        this.token = localStorage.getItem('data')
    }

}


</script>

<style>

</style>