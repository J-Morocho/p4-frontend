<template>
    <form action="">
            <div class="modal-card" style="width: auto">
                <header class="modal-card-head">
                    <p class="modal-card-title">Create a new category</p>
                </header>
                <section class="modal-card-body">
                    <b-field label="Category Name">
                        <b-input type="text" v-model='category_name' maxlength='10' required></b-input>
                    </b-field>
                </section>

                <footer class="modal-card-foot">
                    <button class="button" type="button"  @click="$emit('close')">Close</button>
                    <button class="button is-primary" v-on:click="createCategory">Add</button>
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
            category_name: '',
            credentials: this.user,
            token: '',
            URL: this.url,
        }
    },
    methods: {
        createCategory: function() {
            // After calling this function we need to update categories list in sidebar
            // Let's emit something
            const data = {name: this.category_name} 
            fetch(`${this.URL}/api/categories/`, {
              method: 'post',
              headers: {
                  'Content-Type': 'application/json',
                  'Authorization': `JWT ${this.token}`
              },
              body: JSON.stringify(data)
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
                    this.$emit('add_category_event', data)
                    this.$emit('close')
                }
            })
        },
    },
    beforeMount: function() {
        this.token = localStorage.getItem('data')
    }

}
</script>

<style>

</style>