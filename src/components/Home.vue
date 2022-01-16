<template>
  <Header />
  <div class="homeimg">
    <img src="../assets/resto.jpg" />
  </div>
  <h1>Hello {{ name }}, Wellcome to home page</h1>
  <table border="1">
    <tr>
      <td>Name</td>
      <td>Address</td>
      <td>Contact</td>
      <td>Actions</td>
    </tr>
    <tr v-for="item in resturants" :key="item.id">
      <td>{{ item.name }}</td>
      <td>{{ item.address }}</td>
      <td>{{ item.contact }}</td>
      <td>
        <router-link :to="'/update/' + item.id">Update</router-link>
        <button v-on:click="deleteResturant(item.id)">Delete</button>
      </td>
    </tr>
  </table>
</template>
<script>
import axios from 'axios';
import Header from './Header.vue';
export default {
  name: 'Home',
  data() {
    return {
      name: '',
      resturants: [],
    };
  },
  components: {
    Header,
  },
  methods: {
    async deleteResturant(id) {
      let result = await axios.delete('http://localhost:3000/resturant/' + id);
      if (result.status == 200) {
        this.loadData();
      }
    },
    async loadData() {
      let user = localStorage.getItem('user-info');
      this.name = JSON.parse(user).name;
      if (!user) {
        this.$router.push({ name: 'SignUp' });
      }
      let result = await axios.get('http://localhost:3000/resturant');
      console.warn(result);
      this.resturants = result.data;
    },
  },
  mounted() {
    this.loadData();
  },
};
</script>
<style scoped>
img {
  width: 1340px;
  height: 500px;
  margin-top: 10px;
  margin-left: 10px;
  margin-right: 10px;
}
td {
  width: 160px;
  height: 40px;
}
</style>
