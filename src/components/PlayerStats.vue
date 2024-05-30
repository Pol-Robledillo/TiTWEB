<template>
  <div class="statsBG">
    <div class="statsDisplay">
      <h2>Player Stats</h2>
      <div v-if="playerStats" class="stats">
        <p>Max Points: {{ playerStats.max_points }}</p>
        <p>Total Points: {{ playerStats.total_points }}</p>
        <p>Max Enemies Killed: {{ playerStats.max_enemies_killed }}</p>
        <p>Total Enemies Killed: {{ playerStats.total_enemies_killed }}</p>
      </div>
      <p v-if="message">{{ message }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: ["username"],
  data() {
    return {
      playerStats: null,
      message: "",
      isError: false,
    };
  },
  async created() {
    await this.fetchStats();
  },
  methods: {
    async fetchStats() {
      try {
        const response = await axios.get(
          `https://83bcce6f-98e3-4e59-9aae-4ce96a077b84-00-1zzaaw12iwr1m.picard.replit.dev/players/stats/${this.username}`
        );
        if (response.data) {
          this.playerStats = response.data;
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
.statsBG {
  background-image: url("../assets/valle_primigenio.png");
  background-size: cover;
  height: 923px;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-bottom-left-radius: 10px;
}
.statsDisplay {
  background: #57fdfb;
  width: 300px;
  height: 300px;
  border-radius: 30px;
  border: solid 10px #e4ca7d;
  margin-bottom: 50px;
}
.statsDisplay > h2 {
  font-family: copperplate;
  font-size: 30px;
}
.stats {
  height: 150px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
.stats > p {
  font-family: georgia;
  font-size: 20px;
  margin: 15px;
}
</style>
