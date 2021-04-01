<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>New Post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="newPostTitle" />
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="newPostBody" />
        <small v-if="newPostBody.length > 0">{{ 20 - newPostBody.length }} Characters remaining</small>
        <small v-else-if="newPostBody.length > 20">Body is too long!</small>
      </div>
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="newPostImage" />
      </div>
      <div class="form-group">
        <label>User:</label>
        <input type="text" class="form-control" v-model="newPostUser" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      posts: [],
      newPostTitle: "",
      newPostBody: "",
      newPostImage: "",
      newPostUser: "",
      errors: {},
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
    newPost: function () {
      var params = {
        title: this.newPostTitle,
        body: this.newPostBody,
        image: this.newPostImage,
        user: this.newPostUser,
      };
      axios.post("/api/posts", params).then(() => {
        this.$router.push("/posts");
      });
    },
  },
};
</script>
