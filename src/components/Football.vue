<template>
    <div class="container"> 
      <input type="number" v-model="matchDay" v-on:click="changed()">
<table class="table table-striped mt-4">
  <thead>
    <tr>
      <th scope="col">Home Team</th>
      <th scope="col">Away Team</th>
      <th scope="col">Goal For</th>
      <th scope="col">Goal Against</th>
      <th scope="col">Winner</th>
    </tr>
  </thead>
    <tr v-for="match in matches" v-bind:key="match.id">
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
    competition: "EPL"
  },
  data() {
    return {
      matchDay: 3,
      matches: []
    };
  },
  created() {
    axios
      .get("http://localhost:8088/api/epl/" + this.$data.matchDay)
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
        .get("http://localhost:8088/api/epl/" + this.matchDay)
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
