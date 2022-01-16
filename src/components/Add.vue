<template>
  <Header />

  <h1 class="heading">Add Resturant</h1>
  <form class="add">
    <input
      type="text"
      placeholder="Enter Name"
      v-model="resturant.name"
      name="name"
    />
    <input
      type="text"
      placeholder="Enter Address"
      v-model="resturant.address"
      name="address"
    />
    <input
      type="text"
      placeholder="Enter Contact Number"
      v-model="resturant.contact"
      name="contact"
    />
    <button type="button" v-on:click="addResturant">Add New resturant</button>
  </form>
</template>
<script>
import axios from 'axios';
import Header from './Header.vue';
export default {
  name: 'Add',
  data() {
    return {
      resturant: {
        name: '',
        address: '',
        contact: '',
      },
    };
  },
  methods: {
    async addResturant() {
      console.warn(this.resturant);
      const result = await axios.post('http://localhost:3000/resturant', {
        name: this.resturant.name,
        address: this.resturant.address,
        contact: this.resturant.contact,
      });
      if (result.status == 201) {
        this.$router.push({ name: 'Home' });
      }
      console.warn('result', result);
    },
  },
  components: {
    Header,
  },
  mounted() {
    let user = localStorage.getItem('user-info');
    if (!user) {
      this.$router.push({ name: 'SignUp' });
    }
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
</style>
