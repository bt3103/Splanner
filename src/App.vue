<template>
  <div id="app">
    <div v-if="authenticated == false" class="header">
      <page-header/>
    </div>
    <div v-if="authenticated == true && logout==false" class="header">
      <page-header2/>
    </div>
    <!-- <div id="nav">
      <router-link v-if="authenticated" to="/login" v-on:click.native="Logout();" replace>Logout</router-link>
    </div> -->
    <div class="quotes" v-show="logout"><img src=./assets/quotes.jpg width=100% height=100% /></div>

    <router-view @authenticated="setAuthenticated"/>
    <div class="footer">
      <page-footer/>
    </div>
  </div>
</template>

<script>
import PageHeader from "@/components/Header_login.vue";
import PageHeader2 from "@/components/Header.vue"
import PageFooter from "@/components/Footer.vue";

export default {
  name: "App",
  components: {
    PageHeader,
    PageHeader2
  },
  data() {
    return {
      authenticated: false,
      logout: false,
      mockAccount: {
        username: "A0123456B",
        password: "password"
      }
    };
  },
  mounted() {
    if (!this.authenticated) {
      this.$router.replace({ name: "login" });
    }
  },
  methods: {
    setAuthenticated(status) {
      this.authenticated = status;
    },
    Logout() {
      this.authenticated = false;
      this.logout = true;
    }
  }
};
</script>

<style>
#app {
  margin: auto;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
}
#header {
  color: #2c3e50;
}
</style>
