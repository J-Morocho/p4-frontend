<template>
    <b-navbar class='primary has-background-vegetation'>
        <template slot="brand">
            <b-navbar-item tag="router-link" :to="{ path: '/home' }">
                Plantr
            </b-navbar-item>
        </template>
        <template slot="start">
            <b-navbar-item tag="div">
                <div class="buttons">
                    <router-link to="/">Logout</router-link>
                </div>
            </b-navbar-item>
        </template>
        <template slot="end">
            <hide-at :breakpoints="{medium: 1534}" breakpoint="medium">
                <!-- <Sidebar /> -->
            </hide-at>
            <show-at breakpoint="small">
                <Sidebar :user='credentials' :url='URL'/>
            </show-at>

        </template>

        <!-- <template slot="end">
            <b-navbar-item tag="div">
                <div class="buttons">
                    <router-link to="/">Logout</router-link>
                </div>
            </b-navbar-item>
        </template> -->
    </b-navbar>
</template>

<script>
import Sidebar from './Sidebar.vue'
import {hideAt, showAt} from 'vue-breakpoints'

export default {
  name: "Header",
  props: ['url', 'user'],
  components: {
      Sidebar,
      hideAt,
      showAt
  },
  data: function() {
      return {
          credentials: this.user,
          URL: this.url
      }
  }
};
</script>

<style>
.header {
    width: 90%;
    margin: 10px auto
}

</style>
