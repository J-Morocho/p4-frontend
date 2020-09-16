<template>
    <aside class="menu is-desktop">
        <section class="sidebar-layout">
            <menu>
                <ModalCreateCategory :url='URL' :user='credentials' />
                <div class="p-1">
                    <div class="block">
                    </div>
                        <b-menu-list label="Categories">
                            <div class='category-wrapper' v-for="category in categories" v-bind:key="category.id">
                                <div class="is-active" v-bind:label="category.name" v-bind:id="category.id" v-on:click="setCategoryId">{{category.name}}</div>
                            </div>
                        </b-menu-list>
                    
                </div>
            </menu>
        </section>
    </aside>
</template>

<script>
import ModalCreateCategory from './ModalCreateCategory'

export default {
    name: 'sidebar',
    props: ['url', 'user'],
    components: {
        ModalCreateCategory,
    },
    data: function() {
        return {
            category_id: null,
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
        setCategoryId: function(event) {
            this.category_id = event.target.id
            this.$emit('category_id', this.category_id)
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

ul {
    text-align: left;
}
.menu-label {
    text-align: left;
}

.menu-list {
    padding-bottom: 10px;
}

.menu{
    height: 100vh;
    background-color: #E9E9E9;
}

.category-wrapper {
    padding-bottom: 20px;
}
</style>

