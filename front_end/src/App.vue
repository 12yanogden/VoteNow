<template>
  <div id="app">
    <nav class="navbar is-fixed-top has-shadow" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <router-link to="/" alt="VoteNow" class="navbar-item">
          <img src="./assets/logo_navbar.png" id="logo"/>
        </router-link>

        <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false">
          <span v-if="!user" aria-hidden="true">Create an account</span>
          <span v-if="!user" aria-hidden="true">Sign in</span>
          <span v-if="user" aria-hidden="true" @click.prevent="logout">Logout</span>
        </a>
      </div>
      <div class="navbar-menu">
        <div class="navbar-end">
          <div class="navbar-buttons">
            <button class="navbar-button">Create an account</button>
            <button class="navbar-button">Sign in</button>
            <div v-if="user" class="navbar-item has-dropdown">
              <a class="navbar-link">
                <i class="fas fa-user"></i>
              </a>

              <div class="navbar-dropdown">
                <router-link to="/account" class="navbar-item">
                  My Account
                </router-link>
                <router-link to="/elections" class="navbar-item">
                  Elections
                </router-link>
                <router-link to="/candidates" class="navbar-item">
                  Candidates
                </router-link>
                <hr class="navbar-divider">
                <div class="navbar-item" @click.prevent="logout">
                  Logout
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </nav>
    <div class="wrapper">
      <router-view class="view"/>
    </div>
    <footer class="footer">
      <div class="content center m-5">
        <div class="is-flex is-flex-direction-column">
          <div>
            <strong>VoteNow</strong> by Ryan Ogden
          </div>
          <a id="githubLink" href="https://github.com/12yanogden/VoteNow">
            <i class="fa fa-github fa-2x" aria-hidden="true"></i>
          </a>
        </div>  
      </div>
    </footer>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'app',
  async created() {
    try {
      let response = await axios.get('/api/users');
      this.$root.$data.user = response.data.user;
    } catch (error) {
      this.$root.$data.user = null;
    }
  },
  computed: {
    user() {
      return this.$root.$data.user;
    }
  },
  methods: {
    async logout() {
      try {
        await axios.delete("/api/users");
        this.$root.$data.user = null;
      } catch (error) {
        this.$root.$data.user = null;
      }
    },
  }
}
</script>

<style>
/* Color palette: https://www.schemecolor.com/wp-content/themes/colorsite/include/cc4.php?color0=b42033&color1=cecece&color2=fefefe&color3=3c3b6e&pn=American%20Red,%20White%20and%20Blue */

* {
  box-sizing: border-box;
}

body {
  font-family: 'Work Sans', sans-serif;
  font-weight: 300;
  font-size: 16pt;
  padding: 0;
  margin: 0;
}

.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.row {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.col {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  background: white;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  padding: 20px;
}

.translucent {
  opacity: 0.9;
}

.pointer {
  cursor: pointer;
}

a:link {
  text-decoration: none;
}

.navbar {
  height: 100px;
}

.navbar-item img {
  max-height: initial;
  max-width: 300px;
}

#wrapperLeft {
  margin: 0 1em 0 0;
}

.pure-button-primary {
  background-color: #277E8E;
}

html, body, .app {
  height: 100%;
}

.view {
  min-height: 600px;
}

.wrapper {
  min-height: 100%;
  margin-bottom: -50px;
}

.push {
  height: 50px;
}
</style>
