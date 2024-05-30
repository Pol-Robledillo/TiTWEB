<template>
  <div id="app">
    <header v-if="isLoggedIn">
      <form><button type="button" @click="logOut()">Log Out</button></form>
    </header>
    <div class="statsShowing">
      <login-comp v-if="!isLoggedIn" @login-success="handleLoginSuccess"></login-comp>
      <player-stats v-else :username="username"></player-stats>
      <top-games v-if="isLoggedIn"></top-games>
    </div>
  </div>
</template>

<script>
import LoginComp from "./components/LoginComp.vue";
import PlayerStats from "./components/PlayerStats.vue";
import TopGames from "./components/TopGames.vue";

export default {
  components: {
    LoginComp,
    PlayerStats,
    TopGames,
  },
  data() {
    return {
      isLoggedIn: false,
      username: "",
    };
  },
  methods: {
    handleLoginSuccess(username) {
      this.username = username;
      this.isLoggedIn = true;
    },
    logOut() {
      location.reload();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  width: 100%;
  margin: 0px;
}
.statsShowing {
  display: flex;
}
header {
  height: 30px;
  background-color: gold;
  display: block;
}
form {
  display: flex;
  justify-content: flex-end;
  padding-top: 5px;
  padding-right: 10px;
}
body {
  margin: 0px;
}
</style>
