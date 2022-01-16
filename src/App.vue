<template>
  <router-view />
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body {
  padding: 0;
  margin: 0;
}
.logo {
  width: 70px;
  margin-top: 30px;
  margin-left: 650px;
}
.register input,
.login input,
.add input {
  width: 300px;
  height: 30px;
  padding-left: 20px;
  display: block;
  margin-bottom: 20px;
  margin-left: auto;
  margin-right: auto;
  border: 1.5px solid #ffc206;
  border-radius: 10px;
}
.register button,
.login button,
.add button {
  width: 325px;
  height: 40px;
  border: 1px solid #ffc206;
  color: #fff;
  background-color: #ffc206;
  cursor: pointer;
  margin-left: 520px;
}
.heading {
  text-align: center;
}
</style>
