<template>
  <div id="app">
    <div id="nav" v-if="$route.path !== '/login'">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
    <button @click="logout" v-if="$route.path !== '/login'" class="btn btn-danger logout">Log out</button>
  </div>
</template>
<script>
import { mapActions } from 'vuex'
export default {
  methods: {
    ...mapActions({
      actionLogout: 'auth/logout'
    }),
    logout () {
      this.actionLogout().then((resolve) => {
        alert(resolve)
        window.location = '/login'
      })
    }
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#nav {
  padding: 30px;
  text-align: center;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
.logout {
  position: fixed;
  top: 20px;
  left: 20px;
}
</style>
