<template>
  <div class="home">
    <h1>New Post</h1>
    <div>
      Title:
      <input type="text" v-model="newPostTitle" />
      Body:
      <input type="text" v-model="newPostBody" />
      Image:
      <input type="text" v-model="newPostImage" />
      <button v-on:click="createPost()">Create Post</button>
    </div>
    <h1>All Posts</h1>
    <div v-for="post in posts">
      <img v-bind:src="post.url" v-bind:alt="post.title" />
      <h2>{{ post.title }}</h2>
      <p>Body: {{ post.body }}</p>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to Blogs!",
      posts: [],
      newPostImage: "",
      newPostTitle: "",
      newPostBody: ""
    };
  },
  created: function() {
    axios.get("/api/posts").then(response => {
      this.posts = response.data;
    });
  },
  methods: {
    createPost: function() {
      var params = {
        title: this.newPostTitle,
        image: this.newPostImage,
        body: this.newPostBody
      };
      axios.post("/api/posts", params).then(response => {
        this.posts.push(response.data);
        this.newPostTitle = "";
        this.newPostId = "";
        this.newPostBody = "";
      });
    }
  }
};
</script>