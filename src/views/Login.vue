<template>
    <div class="container">
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
    data: function() {
        return {
            username: 'Sam123',
            password: 'password123',
        }
    },
    methods: {
        handleLogin: function(){
            console.log('click')
            fetch('http://127.0.0.1:8000/auth/users/login/', {
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
                if (response.status == 200) {
                    // Redirect to home if correct credentials are given
                    this.$router.push('/home')
                }
                else {
                    // TODO: HANDLE INCORRECT CREDENTIALS
                    response.json()
                }
            })
        },
    }
}
</script>

<style>
</style>