<template>
  <img class="logo" src="../assets/resto-logo.png" />
  <h1 class="heading">Sign Up</h1>
  <div class="register">
    <input type="text" v-model="name" placeholder="Enter Name" />
    <input type="text" v-model="email" placeholder="Enter Email" />
    <input type="password" v-model="password" placeholder="Enter Password" />
    <button v-on:click="signUp">SignUp</button>
    <p class="heading">
      Already have an Account,<router-link to="/log-in">Login here</router-link>
    </p>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'SignUp',
  data() {
    return {
      name: '',
      email: '',
      password: '',
    };
  },
  methods: {
    async signUp() {
      console.log('signup', this.name, this.email, this.password);
      let result = await axios.post('http://127.0.0.1:3000/user', {
        name: this.name,
        email: this.email,
        password: this.password,
      });
      console.warn(result);
      if (result.status == 201) {
        localStorage.setItem('user-info', JSON.stringify(result.data));
        this.$router.push({ name: 'Home' });
      }
    },
  },
  mounted() {
    let user = localStorage.getItem('user-info');
    if (user) {
      this.$router.push({ name: 'Home' });
    }
  },
};
</script>

<style></style>
