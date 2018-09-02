<template>
    <div class="container"> 
<table class="table table-striped mt-4">
  <thead>
    <tr>
      <th scope="col">Latitude</th>
      <th scope="col">Longitude</th>
    </tr>
  </thead>
    <tr v-for="post in posts" :key="post.id">
        <td>{{post[0]}}</td>
        <td>{{post[1]}}</td>
    </tr>
  <tbody>
    
  </tbody>
</table>
        <button class="btn btn-primary">Universe</button>
    </div>
</template>

<script>
import axios from "axios";
export default {
  name: "PostExample",
  data() {
    return {
      posts: []
    };
  },
  created() {
    
    let systemDt = new Date();
    let formatttedDt = systemDt.getFullYear() + "-";

    let month = systemDt.getMonth() + 1;
    if (month < 10) {
      formatttedDt += "0";
    }
    formatttedDt += month;
    formatttedDt += "-";

    let day = systemDt.getDate();
    if (day < 10) {
      formatttedDt += "0";
    }
    formatttedDt += day;
    formatttedDt += "T";

    let hour = systemDt.getHours();
    if (hour < 10) {
      formatttedDt += "0";
    }
    formatttedDt += hour;
    formatttedDt += ":"

    let minute = systemDt.getMinutes();
    if (minute < 10){
      formatttedDt += "0"
    }
    formatttedDt += minute
    formatttedDt += ":"

    let second = systemDt.getSeconds();
    if (second < 10){
      formatttedDt += "0"
    }
    formatttedDt += second

    //console.log(formatttedDt);
    
    axios
      .get(
        "https://api.data.gov.sg/v1/transport/taxi-availability?date_time=" +
          formatttedDt
      )
      .then(posts => {
        this.posts = posts.data.features[0].geometry.coordinates;
      })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>

<style>
</style>
