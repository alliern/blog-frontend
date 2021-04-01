<template>
  <div class="posts">
    <h1>All Posts</h1>
    <!-- <div v-for="post in posts" v-bind:key="post.id">
      <h1>{{ post.title }}</h1>
      <img v-bind:src="post.image" v-bind:alt="post.title" />
      <router-link v-bind:to="`posts/${post.id}`">More Info</router-link>
    </div> -->
    <div class="card" style="width: 18rem" v-for="post in posts" v-bind:key="post.id">
      <img v-bind:src="post.image" class="card-img-top" alt="post.title" />
      <div class="card-body">
        <h5 class="card-title">{{ post.title }}</h5>
        <router-link v-bind:to="`posts/${post.id}`">More Info</router-link>
      </div>
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
