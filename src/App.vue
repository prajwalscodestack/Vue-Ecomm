<template>
  <div id="container-fluid">
    <!-- <div id="navbar">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> -->
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">CoolTs</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavDropdown">
      <ul class="navbar-nav">
        <li class="nav-item">
          <router-link class="nav-link" to="/">Home</router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link" v-if="$store.state.isAuthenticated" to="/dashboard">Dashboard</router-link>
        </li>
        <li class="nav-item" v-if="!$store.state.isAuthenticated">
          <router-link  class="nav-link" to="/auth/signin">Signin</router-link>
        </li>
        <li class="nav-item" v-if="!$store.state.isAuthenticated">
          <router-link  class="nav-link" to="/auth/signup">Signup</router-link>
        </li>
        <li class="nav-item">
          <router-link v-if="$store.state.isAuthenticated" class="nav-link" to="/products">Products</router-link>
        </li>
        <li class="nav-item">
          <!-- <router-link v-if="isAuthenticated" class="nav-link btn-link" to="/">logout</router-link> -->
          <button v-if="$store.state.isAuthenticated" class="nav-link btn" @click="logout">Logout</button>
        </li>
         <li class="nav-item">
          <!-- <router-link v-if="isAuthenticated" class="nav-link btn-link" to="/">logout</router-link> -->
          <button v-if="$store.state.isAuthenticated" class="btn btn-danger" >Cart {{countCartItems}}</button>
        </li>
        <li v-if="showBuy" class="nav-item">
          <!-- <router-link v-if="isAuthenticated" class="nav-link btn-link" to="/">logout</router-link> -->
          <button v-if="$store.state.isAuthenticated" class="btn btn-danger" >Cart {{countCartItems}}</button>
        </li>
      </ul>
    </div>
  </div>
</nav>
    <router-view/>
  </div>
</template>
<script>
import {mapGetters} from "vuex"
export default {
   computed:{
    ...mapGetters(["countCartItems"])
   },
   methods:{
      logout(){
        this.$session.clear("token")
        this.$session.clear("isAuthenticated")
        this.$session.clear("email")
        this.$store.state.isAuthenticated=false
        this.$router.push("/")
      }
   },
   created(){
      // 
      this.$store.commit('check',this)
   } 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
