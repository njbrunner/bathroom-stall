<template>
  <v-app>
    <v-app-bar
      app
      dense
    >
      <v-toolbar-title>Bathroom Stall</v-toolbar-title>
    </v-app-bar>

    <Post v-for="(post, index) in posts" :key="index" :text=post></Post>

    <NewPost v-if="newPost"></NewPost>

    <v-btn
      fab
      bottom
      right
      fixed
      class="more-margin"
      @click="createNewPost"
    >
      <v-icon>mdi-comment-plus-outline</v-icon>
    </v-btn>
  </v-app>
</template>

<script>
import Post from "@/components/Post.vue";
import NewPost from "@/components/NewPost.vue";

export default {
  name: 'App',
  components: {
    Post,
    NewPost,
  },
  data: () => ({
    posts: ["This is a test post"],
    newPost: false,
  }),
  methods: {
    createNewPost() {
      this.newPost = true;
    }
  },
};
</script>

<style>
.more-margin {
  margin: 32px;
}
</style>
