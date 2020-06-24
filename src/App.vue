<template>
  <v-app>
    <v-app-bar
      app
      dense
    >
      <v-toolbar-title>Bathroom Stall</v-toolbar-title>
    </v-app-bar>

    <TextPost v-for="(post, index) in posts" :key="index" :text=post></TextPost>

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
import TextPost from "@/components/TextPost.vue";

export default {
  name: 'App',
  components: {
    TextPost,
  },
  data: () => ({
    posts: ["This is a test post"],
  }),
  methods: {
    createNewPost() {
      this.posts.push("This is a new dynamically added post.");
    }
  },
};
</script>

<style>
.more-margin {
  margin: 32px;
}
</style>
