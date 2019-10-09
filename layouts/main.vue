<template>
  <div>
    <nav class="navbar is-primary">
      <div id="logo" class="navbar-brand">
        <a class="navbar-item" href="/">
          Meet The Coders
        </a>
        <div class="navbar-burger burger" data-target="navbarExampleTransparentExample">
          <span />
          <span />
          <span />
        </div>
      </div>

      <div id="navbarExampleTransparentExample" class="navbar-menu">
        <div class="navbar-start">
          <a class="navbar-item" href="/">
            Home
          </a>
          <a class="navbar-item" href="/languages">
            Languages
          </a>
        </div>

        <div class="navbar-end">
          <div v-if="isAuthenticated" class="navbar-item has-dropdown is-hoverable">
            <a class="navbar-link" href="#">
              {{ loggedInUser.username }}
            </a>
            <div class="navbar-dropdown">
              <a class="navbar-item" href="/me">
                Profile
              </a>
              <a class="navbar-item" @click="logout">
                Logout
              </a>
            </div>
          </div>
          <template v-else>
            <a class="navbar-item" href="/register">
              Register
            </a>
            <a class="navbar-item" href="/login">
              Login
            </a>
          </template>
        </div>
      </div>
    </nav>
    <nuxt />
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['isAuthenticated', 'loggedInUser'])
  },
  methods: {
    async logout () {
      await this.$auth.logout()
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,700');
html,
body {
  height: 100%;
  width: 100%;
}
body {
  font-family: 'Montserrat', sans-serif;
  font-weight: 300;
  background-color: #fff;
}
* {
  margin: 0;
  padding: 0;
}
ul {
  list-style-type: none;
}
header,
.navbar {
  display: grid;
  grid-template-columns: 20% auto;
}
header a {
  color: white;
  text-decoration: none;
  text-transform: uppercase;
}
#logo {
  font-weight: bold;
  font-size: 1.3em;
  padding: 1.5em 0 2em 0;
  margin: 0;
}
#logo a:hover {
  color: #fff;
}

nav {
  justify-self: right;
}
nav {
  display: inline;
}
nav a {
  padding: 2em;
  display: inline-block;
}
.container {
  width: calc(100% - 4em);
  padding: 2em;
  margin-top: 2em;
}
h1 {
  margin-bottom: 1em;
}

.coder-container,
.coder-container2 {
  background: white;
  border-radius: 7px;
  padding: 1em;
  margin-bottom: 10px;
  display: grid;
  grid-template-columns: 120px auto;
  justify-content: left;
  text-align: left;
  background-color: rgba(65, 184, 131, 0.1);
}
.blank {
  width: 100px;
  height: 100px;
  border: 1px solid lightgray;
  border-radius: 5px;
}
a:hover {
  background: #41b883;
  color: #fff;
}
.navbar-item,
.navbar-link {
  color: #fff;
  font-weight: 700;
}
.navbar-dropdown {
  background-color: #00B89C;
}
#logo:hover {
  background-color: #00B89C;
  color: #fff;
}
</style>
