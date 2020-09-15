<template>
    <aside class="menu">
        <section class="sidebar-layout">
            <menu>
                <div class="p-1">
                    <div class="block">
                    </div>
                    <menu class="is-custom-mobile">
                        <button class="button">Add category</button>
                        <!-- TODO: The label attr gets repeated if it is added in -->
                        <b-menu-list label="Categories" v-for="category in categories" v-bind:key="category.id" >
                            <b-menu-item v-bind:label="category.name" v-bind:id="category.id" v-on:click="displayPlants"></b-menu-item>
                        </b-menu-list>
                    </menu>
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
            fetch(`${this.URL}/api/categories/`, {
                method: 'get',
                headers: {
                    'Authorization': `JWT ${this.token}`
                }
            })
            .then(response => response.json())
            .then(data => this.categories = data.results)
        },
        displayPlants: function() {
            fetch('http://localhost:8000/api/categories/1/plants', {
            method: 'get',
            headers: {
                    'Authorization': `JWT ${this.token}`
                }
            })
            .then(response => response.json())
            .then(data => console.log(data))
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

