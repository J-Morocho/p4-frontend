<template>
    <form action="">
            <div class="modal-card" style="width: auto">
                <header class="modal-card-head">
                    <p class="modal-card-title">Add Plant</p>
                </header>
                <section class="modal-card-body">
                    <b-field label="Plant Information">
                        <b-input type="text" v-bind:plant_name='plant_name' required></b-input>
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
    props: ['canCancel', 'url', 'user', 'cat_id'],
    data: function() {
        return {
            plant_name: '',
            category_id: this.cat_id,
            credentials: this.user,
            token: this.user.token,
            URL: this.url,
        }
    },
    methods: {
        createPlant: function() {
            console.log('click')
            console.log(this.category_id)
            const data = {name: this.plant_name, category: this.category_id} 
            fetch(`${this.URL}/api/plants/`, {
              method: 'post',
              headers: {
                  'Content-Type': 'application/json',
                  'Authorization': `JWT ${this.token}`
              },
              body: JSON.stringify(data)
            })
            .then(response => {
                console.log(response)
                if (response.ok) {
                    response.json()
                } else {
                    return response.json()
                }
            })
            .then(data => {
                if (data) {
                    console.log('data', data)
                    this.$emit('add_plant_event', data)
                    this.$emit('close')
                }
            })

        }
    }

}
</script>

<style>

</style>