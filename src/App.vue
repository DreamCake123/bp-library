<template>
  <div class="app" v-if="loggedIn">
    <Navbar/>
    <router-view class="container"/>
  </div>
  <div class="app" v-else>
    <Login class="mt-5 container"/>
  </div>
</template>

<style lang="scss">
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ccc;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
<script>
  import Navbar from "@/components/Navbar";
  import firebase from 'firebase';
  import Login from "@/views/Login";

  export default {
    components: {Login, Navbar},

    data(){
      return {
        loggedIn: false
      }
    },

    mounted(){
      firebase.auth().onAuthStateChanged(user => {
        this.loggedIn = user;
      })
    }
  }
</script>
