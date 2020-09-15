<template>
    <aside class="menu">
        <section class="sidebar-layout">
            <menu>
                <div class="p-1">
                    <div class="block">
                    </div>
                    <b-menu class="is-custom-mobile">
                        <button class="button">Add category</button>
                        <b-menu-list label="Categories">
                            <b-menu-item icon="logout" label="Category 1"></b-menu-item>
                            <b-menu-item icon="logout" label="Category 2"></b-menu-item>
                        </b-menu-list>
                    </b-menu>
                </div>
            </menu>
        </section>
    </aside>
</template>

<script>
export default {
    name: 'sidebar',
    data: function() {
        return {
            categories: null,
            token: null
        }
    },
    methods: {
        displayCategories: function() {
            fetch('http://localhost:8000/api/categories/', {
                method: 'get',
                headers: {
                    'Authorization': `JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoyLCJ1c2VybmFtZSI6IlNhbTEyMyIsImV4cCI6MTYwNTI5ODU4NCwiZW1haWwiOiJzYW1AZ21haWwuY29tIn0.484wHy70YtjD-nY6gWmbvvT_8T2rBKA_csFrJFd0eQ8`
                }
            })
            .then(response => response.json())
            .then(data => this.categories = data.results)
        },
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

