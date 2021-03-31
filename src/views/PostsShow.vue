<template>
  <div class="posts-show">
    <div class="container">
      <h1>{{ post.title }}</h1>
      <p>{{ post.body }}</p>
      <p>{{ post.user }}</p>
    </div>
    <router-link v-bind:to="`/posts/${post.id}/edit`">Edit</router-link>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      post: [],
    };
  },
  created: function () {
    this.postsShow();
  },
  methods: {
    postsShow: function () {
      axios.get("/api/posts/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.post = response.data;
      });
    },
  },
};
</script>
