<script setup>
import { RouterLink, RouterView } from "vue-router";
import instaGram from "./components/instaGram.vue";
import { reactive, ref } from "vue";
</script>

<template>
  <header>
    <nav>
      <div class="headerImage" @click="$router.push(`/addprofile`)">
        <img
          class="header"
          src="/Users/anorris9/Library/CloudStorage/OneDrive-Humana/Desktop/Capstones/vueInstagramCapstone/vueInstagramCapstone/src/assets/navbar.png"
          alt="tghbrtg"
        />
      </div>
      <RouterLink to="/"></RouterLink>
      <RouterLink to="/addprofile"></RouterLink>
    </nav>
  </header>

  <RouterView></RouterView>

  <footer>
    <img
      class="footer"
      src="/Users/anorris9/Library/CloudStorage/OneDrive-Humana/Desktop/Capstones/vueInstagramCapstone/vueInstagramCapstone/src/assets/IMG_5991.jpg"
    />
  </footer>
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
