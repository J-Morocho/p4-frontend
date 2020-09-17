<template>
    <div class="container has-background-vegetation">
          <h1 class='title is-1'>Plantr</h1>
          <label for='username'>Username</label>
          <input class='input is-primary' type='text' v-model='username'/>

          <label for='password'>Password</label>
          <input class='input is-primary' type='password' v-model='password'/>
          <br>
          <b-button class="is-medium" type="is-info" v-on:click="handleLogin" rounded>Login</b-button>
          <br>
          <b-button class="is-medium"
                    tag="router-link" 
                    to="/register"
                    type="is-info" 
                    rounded> Register</b-button>
    </div>
</template>

<script>
export default {
    name: 'Login',
    props: ['url'],
    data: function() {
        return {
            username: '',
            password: '',
            URL: this.url
        }
    },
    methods: {
        handleLogin: function(){
            fetch(`${this.URL}/auth/users/login/`, {
                method: 'post',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    username: this.username,
                    password: this.password
                })
            })
            .then(response => 
            {
                if (!response.ok) {
                    // When response.ok = false
                    // Handle incorrect login credentials
                    response.json()
                } else {
                    return response.json()
                }
            }
            )
            .then(data => {
                if (data) {
                    this.$emit('loggedIn', data)
                } else {
                    alert('Incorrect login')
                }
            })
        },
    }
}
</script>

<style>
.container {
    height: 100vh;
}
</style>