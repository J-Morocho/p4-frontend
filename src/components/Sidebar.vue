<template>
    <aside class="menu is-desktop">
        <section class="sidebar-layout">
            <menu>
                <ModalCreateCategory class="cst-btn" :url='URL' :user='credentials' @add_category_event='displayCategories'/>
                <div class="p-1">
                    <b-menu-list class="menu-list" label="Categories">
                        <div class='category-wrapper is-active' v-for="category in categories" v-bind:key="category.id">
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
            token: '',
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
            localStorage.setItem('categoryId', event.target.id)
            this.category_id = event.target.id
            this.$emit('category_id', this.category_id)
        }
    },
    beforeMount: function() {
        this.token = localStorage.getItem('data')
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

menu {
    padding: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.menu{
    height: 100vh;
    background-color: #E9E9E9;
}


.category-wrapper {
    padding-bottom: 20px;
}

.cst-btn {
    padding: 20px;
}
</style>

