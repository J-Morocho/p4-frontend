<template>
    <b-navbar class='primary has-background-vegetation'>
        <template slot="brand">
            <b-navbar-item tag="router-link" :to="{ path: '/home' }">
                Plantr
            </b-navbar-item>
        </template>
        <template slot="start">
            <!-- TODO: FIX ON MOBILE AND DESKTOP 
            SLOT START CAUSES THE WHOLE SIDEBAR TO DISPLAY ON THE NAVBAR
            WE NEED TO HIDE THE DESKTOP SIDEBAR WHEN ON MOBILE.
            WE CAN GENERATE CATEGORIES ON THE FLY IN HERE THEN HIDE THEM
            IF ON DESKTOP-->
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
