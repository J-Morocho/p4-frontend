<template>
    <div class="container has-background-vegetation">
          <h1 class='title is-1'>Plantr</h1>
          <label for='username'>Username</label>
          <input class='input is-primary' type='text' v-model='username'/>

          <label for='password'>Password</label>
          <input class='input is-primary' type='password' v-model='password'/>
          <!-- <b-field>
                <b-input type="password"
                    placeholder="Password reveal input"
                    password-reveal>
                </b-input>
          </b-field> -->
          <br>
          <router-link to="" v-on:click.native="handleLogin">Login</router-link>
          <br>
          <router-link to="/register" tag="button">Register</router-link>
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
            link: this.url
        }
    },
    methods: {
        handleLogin: function(){
            fetch(`${this.link}/auth/users/login/`, {
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
                if (response.status !== 200) {
                    // Handle incorrect login
                    return response.json()
                } else {
                    return response.json()
                }
            }
            )
            .then(data => {
                console.log('data',data)
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