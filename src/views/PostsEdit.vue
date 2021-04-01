<template>
  <div class="signup">
    <form v-on:submit.prevent="postsEdit(post)">
      <h1>New Post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="title" />
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="body" />
      </div>
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="image" />
      </div>
      <div class="form-group">
        <label>User:</label>
        <input type="text" class="form-control" v-model="user" />
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
      post: [],
    };
  },
  created: function () {
    axios.get("/api/posts/" + this.$route.params.id);
  },
  methods: {
    postsEdit: function (post) {
      var params = {
        title: post.title,
        body: post.body,
        image: post.image,
        user: post.user,
      };
      axios.patch("/api/posts" + this.post.id, params).then(() => {
        console.log("Updating");
        this.$router.push("/posts");
      });
    },
  },
};
</script>
