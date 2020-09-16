<template>
    <form action="">
            <div class="modal-card" style="width: auto">
                <header class="modal-card-head">
                    <p class="modal-card-title">Add Plant</p>
                </header>
                <section class="modal-card-body">
                    <b-field label="Plant Information">
                        <b-input type="text" v-bind:category_name='category_name' required></b-input>
                    </b-field>
                </section>

                <footer class="modal-card-foot">
                    <button class="button" type="button"  @click="$emit('close')">Close</button>
                    <button class="button is-primary" :click="createCategory">Add</button>
                </footer>
            </div>
        </form>
</template>

<script>
export default {
    name: 'ModalFormPlant',
    props: ['canCancel', 'url', 'user'],
    data: function() {
        return {
            category_id: null,
            credentials: this.user,
            token: this.user.token,
            URL: this.url,
        }
    },
    methods: {
        createCategory: function() {
            const data = {name: this.category_name} 
            fetch(`${this.URL}/api/categories/${this.category_id}/plants`, {
              method: 'post',
              headers: {
                  'Content-Type': 'application/json',
                  'Authorization': `JWT ${this.token}`
              },
              body: JSON.stringify(data)
            })
            .then(response => response.json())
            .then(data => console.log(data))

        }
    }

}
</script>

<style>

</style>