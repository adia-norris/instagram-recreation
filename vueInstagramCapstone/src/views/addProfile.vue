<script setup>
import { reactive, ref } from "vue";
import { useRouter } from "vue-router";
import instaGram from "@/components/instaGram.vue";

const router = useRouter();

const username = ref("");
const likes = ref("");
const postimage = ref("");
const caption = ref("");
const userimage = ref("");
const id = ref("");

function addProfile() {
  const post = {
    username: username.value,
    userimage: userimage.value,
    postimage: postimage.value,
    caption: caption.value,
    likes: likes.value,
    id: id.value,
  };
  const params = {
    method: "POST",
    headers: {
      Accept: "application/json",
      "Content-Type": "application/json",
    },
    body: JSON.stringify(post),
  };

  fetch("https://66ccd18b8ca9aa6c8cc8cbc0.mockapi.io/post", params)
    .then((response) => response.json())
    .then((profile) => {
      router.push("/");
    });
}
</script>

<template>
  <div>
    <br /><br /><br /><br />
    <h1 class="newPost">
      Create a New Post Here! <br /><br />
      <label for="username">Username </label>
      <input
        type="text"
        placeholder="Username"
        id="username"
        v-model="username"
      />
      <br /><br />

      <label for="userImage">Post Your Profile Pic: </label>
      <input type="text" placeholder="URL" id="userImage" v-model="userimage" />
      <br /><br />

      <label for="postImage">Post Your Image Here: </label>
      <input type="text" placeholder="URL" id="postImage" v-model="postimage" />
      <br /><br />

      <label for="caption">Tell us about your post: </label>
      <input type="text" placeholder="caption" id="caption" v-model="caption" />
      <br /><br />

      <label for="likes"># of Likes ❤️ </label>
      <input
        type="number"
        placeholder="How likeable are you?"
        id="likes"
        v-model="likes"
      />
      <br />
    </h1>
  </div>
  <button @click="addProfile(username, userimage, postimage, caption, likes)">
    Add Post
  </button>
  <br /><br /><br /><br />
</template>

<style scoped></style>

<!-- In part 3 we will add the ability for a user to like a post. You should add a "like" button to the left of the likes on a post. When a user clicks the button your website should make a PUT request to the API. The PUT request body should include the new number of likes. If a user has already liked a post they should be able to unlike a post. Unliking a post will send a PUT request to API including the updated number of likes. Liking and unliking a post should update not only the UI in your app but also the value of the likes in the database. You can find some useful hints a resources below:

Resources: 
https://main--creative-youtiao-e1f298.netlify.app/ - example app of finished functionality 

POST URL
https://66ccd18b8ca9aa6c8cc8cbc0.mockapi.io/post/{POST_ID}.  - you will need to replace {POST_ID} with the ID of the post you want to update the likes on. This is the URL you will use for your fetch.

Tips:
Remember this will use a PUT request. PUT is used when we want to update data. 
You can use a v-if to display the correct like button
You can use css to apply a grey filter to an image -->
