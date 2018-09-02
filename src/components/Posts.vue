<template>
    <div class="container"> 
<table class="table table-striped mt-4">
  <thead>
    <tr>
      <th scope="col">User Id</th>
      <th scope="col">Id</th>
      <th scope="col">Title</th>
      <th scope="col">Body</th>
    </tr>
  </thead>
    <tr v-for="post in posts" :key="post.id">
        <td>{{post.userId}}</td>
        <td>{{post.id}}</td>
        <td>{{post.title}}</td>
        <td>{{post.body}}</td>
    </tr>
  <tbody>
    
  </tbody>
</table>
        <button class="btn btn-primary">Universe</button>
    </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "PostExample",
  data() {
    return {
      posts: [
        /*
            {id:1,title:'Post 1',body:'The Body'},
            {id:2,title:'Post 2',body:'The Body'},
            {id:3,title:'Post 3',body:'The Body'},
            {id:4,title:'Post 4',body:'The Body'}
            */
      ]
    };
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/posts').then(posts=>{ this.posts = posts.data})
  }
};
</script>

<style>
</style>
