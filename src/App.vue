<template>
  <v-app>
    <v-app-bar app dense>
      <v-toolbar-title>Bathroom Stall</v-toolbar-title>
    </v-app-bar>

    <stall></stall>
    <v-btn fab bottom right fixed class="more-margin" @click="createNewPost">
      <v-icon>mdi-comment-plus-outline</v-icon>
    </v-btn>
  </v-app>
</template>

<script>
import Stall from "@/components/Stall.vue";
export default {
  name: "App",
  components: {
    // Post,
    // NewPost,
    Stall,
  },
  data: () => ({
    newPost: false,
  }),
  methods: {
    createNewPost() {
      // this.newPost = true;
      this.panZoomObject.pan(0, 0);
    },
  },
};
</script>

<style>
body,
html {
  position: fixed;
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}
</style>
