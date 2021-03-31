<template>
  <div class="posts">
    <div v-for="post in posts" v-bind:key="post.id">
      <h1>{{ post.title }}</h1>
      <router-link v-bind:to="`posts/${post.id}`">More Info</router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      posts: [],
    };
  },
  created: function () {
    this.postsIndex();
  },
  methods: {
    postsIndex: function () {
      axios.get("/api/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
