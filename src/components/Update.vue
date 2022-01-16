<template>
  <Header />

  <h1 class="heading">Update Resturant</h1>
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
    <button type="button" v-on:click="updateResturant">Update resturant</button>
  </form>
</template>
<script>
import axios from 'axios';
import Header from './Header.vue';
export default {
  name: 'Update',
  components: {
    Header,
  },
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
    async updateResturant() {
      const result = await axios.put(
        'http://localhost:3000/resturant/' + this.$route.params.id,
        {
          name: this.resturant.name,
          address: this.resturant.address,
          contact: this.resturant.contact,
        }
      );
      if (result.status == 200) {
        this.$router.push({ name: 'Home' });
      }
    },
  },
  async mounted() {
    let user = localStorage.getItem('user-info');
    if (!user) {
      this.$router.push({ name: 'SignUp' });
    }
    const result = await axios.get(
      'http://localhost:3000/resturant/' + this.$route.params.id
    );
    this.resturant = result.data;
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
