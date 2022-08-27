<template>
  <div class="home">
    <div v-if="!user" class="card">
      <h2>Welcome!</h2>
      {{ user }}
      <p>You're not logged in. Please sign in, or register if you don't have an account</p>
      <router-link to="/register">Register</router-link>
      <router-link to="/login">Login</router-link>
    </div>

    <div v-if="user" class="card">
      <h3>Hello {{ user.name }}!</h3>
      <p>Your email is {{ user.email }}</p>
      <a href="/">Log out</a>
    </div>

  </div>

</template>

<script>
export default {
  props: ['user']
}

</script>

<style scoped>
.card {
  width: 50vw;
  margin: 3rem auto;
  background: rgba(230, 230, 230, .4);
  padding: 2rem;
}

h2 {
  font-size: 2.3rem;
}

p {
  font-size: 1.2rem;
  margin-bottom: 2rem;
}

a {
  color: #fff;
  background: #23ce23;
  padding: 10px 15px;
  text-decoration: none;
  margin: 10px;
}

div h3, div p{
  text-align: left;
}
</style>
