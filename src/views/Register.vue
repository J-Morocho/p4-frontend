<template>
    <div class="container has-background-vegetation">
          <h1 class='title is-1'>Plantr</h1>
          <label for='username'>Username</label>
          <input class='input' type='text' v-model='username'/>

          <label for='first_name'>First Name</label>
          <input class='input' type='text' v-model='first_name'/>

          <label for='last_name'>last_name</label>
          <input class='input is-primary' type='text' v-model='last_name'/>

          <label for='password'>Password</label>
          <input class='input is-primary' type='password' v-model='password'/>

          <label for='email'>Email</label>
          <input class='input is-primary' type='email' v-model='email'/>           
          <!-- Redirect once status OK is recieved -->
          <br>
          
          <b-button class="is-medium"
                    tag="router-link" 
                    to="/register"
                    type="is-info" 
                    v-on:click.native="handleRegistration" 
                    rounded> Register</b-button>
          <br>
          <label for='login'>Have an account? Log in instead:</label>
          <b-button class="is-medium" type="is-info" tag="router-link" to="/" rounded>Login</b-button>
    </div>
</template>


<script>
export default {
    name: 'Register',
    props: ['url'],
    data: function() {
        return {
            username: null,
            first_name: null,
            last_name: null,
            password: null,
            email: null,
            URL: this.url
        }
    },
    methods: {
        handleRegistration: function() {
            fetch(`${this.URL}/auth/users/register/`, {
                method: 'post',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    username: this.username,
                    first_name: this.first_name,
                    last_name: this.last_name,
                    password: this.password,
                    email: this.email
                })
            })
            .then(response => {
                if (response.ok) {
                    return response.json()
                } else {
                    alert('something went wrong')
                }
            })
            .then(data => {
                if (data) {
                    this.$router.push('/home')
                }
            })
        }
    }
}
</script>

<style>

</style>