<template>
  <div class="loginBG">
    <h1>Time is Ticking!</h1>
    <div class="formBG">
      <h2>Login</h2>
      <form @submit.prevent="login">
        <input type="text" v-model="username" placeholder="Username" required />
        <input type="password" v-model="password" placeholder="Password" required />
        <button type="submit">Login</button>
      </form>
      <p v-if="message">{{ message }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      username: "",
      password: "",
      message: "",
      isError: false,
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post(
          "https://83bcce6f-98e3-4e59-9aae-4ce96a077b84-00-1zzaaw12iwr1m.picard.replit.dev/players/login",
          {
            name: this.username,
            pwd_hash: this.password,
          }
        );
        if (response.data.message === "Login successful") {
          this.$emit("login-success", this.username);
        } else {
          this.message = response.data.error;
          this.isError = true;
        }
      } catch (error) {
        this.message = "An error occurred. Please try again later.";
        this.isError = true;
        console.error("Error:", error);
      }
    },
  },
};
</script>

<style scoped>
.loginBG {
  width: 100%;
  height: 953px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-image: url("../assets/valle_primigenio.png");
  background-size: cover;
}
h1 {
  margin-bottom: 100px;
  color: orange;
  font-size: 50px;
}
.formBG {
  display: flex;
  justify-content: center;
  flex-direction: column;
  background-color: #2c70ff;
  width: 200px;
  height: auto;
  border: solid 5px #8e732e;
  border-radius: 20px;
}

form {
  width: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 5px;
  margin-top: 0px;
}
form > input {
  margin-bottom: 3px;
}
form > button {
  margin-top: 10px;
  padding: 5px;
  width: auto;
}
h2 {
  font-family: copperplate;
  font-size: 30px;
  font-weight: bold;
  color: #edb210;
}
</style>
