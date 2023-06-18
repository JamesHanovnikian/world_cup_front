<template>
  <div class="home">
    <h1> World Cup Predictor - Qatar </h1>


    {{ currentGroup["teams"] }}
     
    <div class="table-header"> 
      <button v-on:click="showTournamentGroup(1)"> Group A </button> 
      <button v-on:click="showTournamentGroup(2)"> Group B </button> 
      <button v-on:click="showTournamentGroup(3)"> Group C </button> 
      <button v-on:click="showTournamentGroup(4)"> Group D </button> 
      <button v-on:click="showTournamentGroup(5)"> Group E </button> 
      <button v-on:click="showTournamentGroup(6)"> Group F </button> 
      <button v-on:click="showTournamentGroup(7)"> Group G </button> 
      <button v-on:click="showTournamentGroup(8)"> Group H </button> 
    </div>  
      <table>
        <tr>
        <th> Country </th> 
        <th> Pts </th>
        <th> MP </th>
        <th> W </th>
        <th> L </th>
        <th> GF </th>
        <th> GA</th>
        <th> +/- </th>  
      </tr>
      <tr v-for="team in currentGroup.teams">
        <th> {{ team.name }}</th> 
        <th> {{ team.total_points }}</th> 
        <th> </th> 
        <th> {{  team.group_wins }}</th> 
        <th> {{ team.group_losses }}</th> 
        <th> {{ team.goal_diff }}</th> 
      </tr>
    </table>
  </div>
</template>

<style>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;

  width: 60%;
}
.groups {
  display: flex;
}
td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

.table-header {
  display: flex;
  width: 60%;
  justify-content: center;
}

.table-header a {
  padding: 8px;
}
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      matches: [],
      teams: [],
      tournamentGroups: [],
      currentGroup: [],
    };
  },
  created: function () {
    this.indexTournamentGroups();
  },
  methods: {
    indexMatches: function () {
      axios.get("/matches").then((response) => {
        console.log("Matches index", response);
        this.matches = response.data;
      });
    },
    indexTeams: function () {
      axios.get("/teams").then((response) => {
        console.log("Teams Index", response);
        this.teams = response.data;
      });
    },
    indexTournamentGroups: function () {
      axios.get("/tournament_groups").then((response) => {
        console.log("Tournie Groups!!", response);
        this.tournamentGroups = response.data;
      });
    },
    showTournamentGroup: function (id) {
      console.log("show Tourament", id);
      axios.get("tournament_groups/" + id).then((response) => {
        console.log("Show tournie", response);
        this.currentGroup = response.data;
      });
    },
  },
};
</script>
