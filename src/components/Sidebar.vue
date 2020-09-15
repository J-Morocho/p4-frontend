<template>
    <aside class="menu">
        <section class="sidebar-layout">
            <menu>
                <div class="p-1">
                    <div class="block">
                    </div>
                        <button class="button">Add category</button>
                        <b-menu-list label="Categories">
                            <div v-for="category in categories" v-bind:key="category.id">
                                <div v-bind:label="category.name" v-bind:id="category.id" :click="setCategoryId">{{category.name}}</div>
                            </div>
                        </b-menu-list>
                    
                </div>
            </menu>
        </section>
    </aside>
</template>

<script>
export default {
    name: 'sidebar',
    props: ['url', 'user'],
    data: function() {
        return {
            categories: null,
            credentials: this.user,
            token: this.user.token,
            URL: this.url
        }
    },
    methods: {
        displayCategories: function() {
            // Used to list out category names as a list
            fetch(`${this.URL}/api/categories/`, {
                method: 'get',
                headers: {
                    'Authorization': `JWT ${this.token}`
                }
            })
            .then(response => response.json())
            .then(data => this.categories = data.results)
        },
        setCategoryId: function() {
            // fetch(`${this.URL}/api/categories/${this.categ}/plants`, {
            // method: 'get',
            // headers: {
            //         'Authorization': `JWT ${this.token}`
            //     }
            // })
            // .then(response => response.json())
            // .then(data => console.log(data))
            console.log('click')
            console.log('a')
            //this.$emit('category_id', this.category_id)
        }
    },
    beforeMount: function() {
        this.displayCategories()
    }
}
</script>

<style>

.p-1 {
    background-color: #E9E9E9;
}

.menu{
    height: 100vh;
    background-color: #E9E9E9;;
};
</style>

