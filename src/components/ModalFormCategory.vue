<template>
    <form action="">
            <div class="modal-card" style="width: auto">
                <header class="modal-card-head">
                    <p class="modal-card-title">Create a new category</p>
                </header>
                <section class="modal-card-body">
                    <b-field label="Category Name">
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
    name: 'ModalFormCategory',
    props: ['canCancel', 'url', 'user'],
    data: function() {
        return {
            category_name: null,
            credentials: this.user,
            token: this.user.token,
            URL: this.url,
        }
    },
    methods: {
        createCategory: function() {
            const data = {name: this.category_name} 
            fetch(`${this.URL}/api/categories/`, {
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