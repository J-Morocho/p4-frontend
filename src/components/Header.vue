<template>
    <b-navbar class='primary'>
        <template slot="brand">
            <b-navbar-item tag="router-link" :to="{ path: '/' }">
                Plantr
            </b-navbar-item>
        </template>
        <!-- Will need to add categories in here -->
        <template slot="start">
        </template>

        <template slot="end">
            <b-navbar-item tag="div">
                <div class="buttons">
                    <a class="button is-light">
                        Log out
                    </a>
                </div>
            </b-navbar-item>
        </template>
    </b-navbar>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style>
.header {
    width: 90%;
    margin: 10px auto
}

b-navbar {
  background-color: green;
}
</style>
