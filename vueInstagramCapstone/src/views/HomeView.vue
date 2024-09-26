<script setup>
import { RouterLink, RouterView } from "vue-router";
import instaGram from "../components/instaGram.vue";
import { reactive } from "vue";
import { ref } from "vue";
import addProfile from "./addProfile.vue";

const postDetails = reactive([]);

fetch("https://66ccd18b8ca9aa6c8cc8cbc0.mockapi.io/post")
  .then((response) => {
    return response.json();
  })

  .then((profile) => {
    postDetails.value = profile;
  });
</script>

<template>
  <body>
    <instaGram
      v-for="post in postDetails.value"
      :profile="post"
      :key="post.id"
    ></instaGram>
  </body>
</template>

<style scoped>
.header {
  height: 275px;
  display: flex;
  flex-direction: column;
}
.addBar {
  width: 600px;
}
.footer {
  height: 110px;
}

body {
  display: flex;
  flex-direction: column;
  width: 600px;
}
</style>
