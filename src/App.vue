<template>
  <div class="container">
    <nav>
      <div class="nav-left">
        <h2>Login App</h2>
      </div>

      <div class="nav-right">
        <router-link to="/" >Home</router-link>
        <router-link to="/register">Register</router-link>
        <router-link to="/login">Login</router-link>
      </div>
    </nav>

    <router-view @loggedIn="setUser" :user="user" />

  </div>


</template>

<script>

export default {
  data() {
    return {
      user: '',
    }
  },
  methods: {
    setUser(user){
      this.user = user
      console.log(this.user)
    }
  }
  
}
</script>

<style>
#app {
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  width: 80vw;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 0 8rem;
}

.nav-right {
  padding: 1.5rem 3rem;
}

nav a {
  font-weight: bold;
  margin-left: 5rem;
  text-decoration: none;

  color: #333;
}

nav a.router-link-exact-active {
  color: #23ce23;
}
</style>
