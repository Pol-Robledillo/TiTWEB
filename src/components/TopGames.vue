<template>
  <div class="leaderBoardBG">
    <div class="scoresDisplay">
      <h3>Leaderboard</h3>
      <ul>
        <li v-for="game in topGames" :key="game.id">
          Points: {{ game.points }}, Enemies Killed: {{ game.enemies_killed }}, Level:
          {{ game.level }}, Date: {{ game.date }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      topGames: [],
      message: "",
      isError: false,
    };
  },
  async created() {
    await this.fetchTopGames();
  },
  methods: {
    async fetchTopGames() {
      try {
        const response = await axios.get(
          "https://83bcce6f-98e3-4e59-9aae-4ce96a077b84-00-1zzaaw12iwr1m.picard.replit.dev/games/top"
        );
        if (response.data) {
          this.topGames = response.data;
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
.leaderBoardBG {
  background-image: url("../assets/servington.png");
  background-size: cover;
  height: 923px;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.scoresDisplay {
  background: #57fdfb;
  width: 800px;
  height: auto;
  border-radius: 30px;
  border: solid 10px #e4ca7d;
  margin-bottom: 50px;
  padding-right: 30px;
}
ul > li {
  font-family: georgia;
  font-size: 20px;
}
ul {
  list-style: none;
}
.imgs {
  width: 70%;
  display: flex;
  justify-content: space-around;
  padding-top: 30px;
}
</style>
