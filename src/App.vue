<template>
  <div id="app">
    <header id="fh5co-header" role="banner">
      <div class="container">
        <div class="header-inner">
          <h1><router-link to="/movies">Movies</router-link></h1>
          <nav role="navigation">
            <ul>
              <li><router-link to="/movies/new">New</router-link></li>
              <li v-if="!isLoggedIn()">
                <router-link to="/login">Login</router-link>
              </li>
              <li v-if="isLoggedIn()">
                <router-link to="/logout">Logout</router-link>
              </li>
              <li v-if="!isLoggedIn()" class="cta">
                <router-link to="/signup">Signup</router-link>
              </li>
            </ul>
          </nav>
        </div>
      </div>
    </header>

    <router-view />
  </div>
</template>

<script>
export default {
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
