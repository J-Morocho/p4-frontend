<template>
    <div class="container">
          <h1 class='title is-1'>Plantr</h1>
          <label for='username'>Username</label>
          <input class='input is-primary' type='text' v-model='username'/>
          <!-- <label for='first_name'>First Name</label>
          <input class='input is-primary' type='text' v-model='first_name'/>
          <label for='last_name'>Last Name</label>
          <input class='input is-primary' type='password' v-model='last_name'/>
          <label for='email'>Email</label>
          <input class='input is-primary' type='email' v-model='email'/> -->
          <label for='password'>Password</label>
          <input class='input is-primary' type='password' v-model='password'/>
          <!-- <b-field>
                <b-input type="password"
                    placeholder="Password reveal input"
                    password-reveal>
                </b-input>
          </b-field> -->
          <br>
          <router-link to="/" tag="button">Login</router-link>
          <br>
          <button class='button'>Register</button>
          <router-view/>
        </div>
</template>

<script>
export default {
    name: 'Login',
}
</script>

<style>
</style>