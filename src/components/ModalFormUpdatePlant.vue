<template>
    <form action="">
            <div class="modal-card" style="width: auto">
                <header class="modal-card-head">
                    <p class="modal-card-title">Update Plant</p>
                </header>
                <section class="modal-card-body">
                    <b-field label="Plant Information">
                        <b-input type="text" v-bind:category_name='category_name' required></b-input>
                    </b-field>
                </section>

                <footer class="modal-card-foot">
                    <button class="button" type="button"  @click="$emit('close')">Close</button>
                    <button class="button is-primary" :click="updatePlant">Update</button>
                </footer>
            </div>
        </form>
</template>

<script>
export default {
    name: 'ModalFormUpdatePlant',
    props: ['canCancel', 'url', 'user'],
    data: function() {
        return {
            plant_id: null,
            name: null,
            // Will need to update watered count
            is_watered: null,
            category_id: null,
            credentials: this.user,
            token: '',
            URL: this.url,
        }
    },
    methods: {
        updatePlant: function() {
            const data = {name: this.name, is_watered: this.is_watered, category: this.category_id} 
            fetch(`${this.URL}/api/plants/${this.plant_id}/`, {
              method: 'PUT',
              headers: {
                  'Content-Type': 'application/json',
                  'Authorization': `JWT ${this.token}`
              },
              body: JSON.stringify(data)
            })
            .then(response => response.json())
            .then(data => console.log(data))

        }
    },
    beforeMount: function() {
        this.token = localStorage.getItem('data')
    }

}
</script>

<style>

</style>