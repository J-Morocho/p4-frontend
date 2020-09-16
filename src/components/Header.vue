<template>
    <b-navbar class='primary has-background-vegetation'>
        <template slot="brand">
            <b-navbar-item tag="router-link" :to="{ path: '/home' }">
                Plantr
            </b-navbar-item>
        </template>
        <!-- Will need to add categories in here -->
        <template slot="start">
            <Sidebar />
        </template>

        <template slot="end">
            <b-navbar-item tag="div">
                <div class="buttons">
                    <router-link to="/">Logout</router-link>
                </div>
            </b-navbar-item>
        </template>
    </b-navbar>
</template>

<script>
import Sidebar from './Sidebar.vue'
export default {
  name: "Header",
  components: {
      Sidebar
  }
};
</script>

<style>
.header {
    width: 90%;
    margin: 10px auto
}

</style>
