<template>
    <div class="container" v-on:change="changed()"> 
      <select v-model="competition">
  <option value="BSA">Brazilian Division One</option>
  <option value="PL">English Premiere League</option>
  <option value="ELC">Championship</option>
  <option value="CL">Champions League</option>
  <option value="EC">European Championships</option>
  <option value="FL1">France League 1</option>

  <option value="BL1">Bundesliga</option>
  <option value="SA">Italy Serie A</option>
  <option value="DED">Eredivise</option>
  <option value="PPL">Portuguese Primera Division</option>
  <option value="PD">Primera Division</option>
  <option value="WC">World Cup</option>
</select>
  <input type="number" v-model="matchDay" v-on:click="changed()">
<table class="table table-striped mt-4">
  <thead>
    <tr>
      <th scope="col">Last Updated</th>
      <th scope="col">Home Team</th>
      <th scope="col">Away Team</th>
      <th scope="col">Goal For</th>
      <th scope="col">Goal Against</th>
      <th scope="col">Winner</th>
    </tr>
  </thead>
    <tr v-for="match in matches" v-bind:key="match.id">
        <td>{{match.utcDate}}</td>
        <td>{{match.homeTeam.name}}</td>
        <td>{{match.awayTeam.name}}</td>
        <td>{{match.score.fullTime.homeTeam}}</td>
        <td>{{match.score.fullTime.awayTeam}}</td>
        <td>{{match.score.winner}}</td>
    </tr>
  <tbody>
    
  </tbody>
</table>
        
    </div>
</template>

<script>
import axios from "axios";
export default {
  name: "PostExample",
  props: {
   
  },
  data() {
    return {
      matchDay: 3,
      competition: "PL",
      matches: []
    };
  },
  created() {
    axios
      .get(
        "http://localhost:8080/api/football/comp/" +
          this.competition +
          "/" +
          this.matchDay
      )
      .then(posts => {
        this.matches = posts.data.matches;
      })
      .catch(error => {
        console.log(error);
      });
  },

  methods: {
    changed(event) {
      console.log(this.matchDay);

      axios
        .get(
          "http://localhost:8080/api/football/comp/" +
            this.competition +
            "/" +
            this.matchDay
        )
        .then(posts => {
          this.matches = posts.data.matches;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style>
</style>
