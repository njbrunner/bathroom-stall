<template>
  <v-app>
    <v-app-bar
      app
      dense
    >
      <v-toolbar-title>Bathroom Stall</v-toolbar-title>
    </v-app-bar>

    <TextPost></TextPost>

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
    //
  }),
};
</script>
