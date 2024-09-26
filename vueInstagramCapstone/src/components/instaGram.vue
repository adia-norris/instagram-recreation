<script setup>
import { reactive, ref } from "vue";
import { useRoute } from "vue-router";
import addProfile from "@/views/addProfile.vue";
//name of the prop matters in your v-for statement in the template. nowhere else. :-()

const props = defineProps(["profile"]);
const emits = defineEmits(["update"]);

const isLiked = ref(false);

function addLike() {
  isLiked.value = true;
  updateDatabase(props.profile.likes++);
}

function unlike() {
  isLiked.value = false;
  updateDatabase(props.profile.likes--);
}

function updateDatabase(likeCount) {
  const body = {
    likes: likeCount,
  };
  const params = {
    method: "PUT",
    headers: {
      Accept: "application/json",
      "Content-Type": "application/json",
    },
    body: JSON.stringify(body),
  };
  fetch(
    `https://66ccd18b8ca9aa6c8cc8cbc0.mockapi.io/post/${props.profile.id}`,
    params
  )
    .then((response) => response.json())
    .then((data) => {
      console.log(data);
    });
}
</script>

<template>
  <div class="igCardContainer">
    <div class="userInfo">
      <img class="profilePic" :src="profile.userimage" alt="profile pic" />
      <p class="userName">{{ profile.username }}</p>
      <h1 class="kebab">...</h1>
    </div>

    <div class="postImage">
      <img class="imagePosted" :src="profile.postimage" alt="image post" />
    </div>

    <div class="likesContainer">
      <img
        @click="addLike()"
        v-if="!isLiked"
        class="unfilledHeart"
        src="/Users/anorris9/Library/CloudStorage/OneDrive-Humana/Desktop/Capstones/vueInstagramCapstone/vueInstagramCapstone/src/assets/unfilledheart.png"
        alt=""
      />
      <img
        @click="unlike()"
        v-else
        class="filledHeart"
        src="/Users/anorris9/Library/CloudStorage/OneDrive-Humana/Desktop/Capstones/vueInstagramCapstone/vueInstagramCapstone/src/assets/filledheart.png"
        alt=""
      />
      <h3 class="likes">{{ profile.likes }}</h3>
      <img
        class="comment"
        src="/Users/anorris9/Library/CloudStorage/OneDrive-Humana/Desktop/Capstones/vueInstagramCapstone/vueInstagramCapstone/src/assets/comment.png"
        alt=""
      />
      <img
        class="message"
        src="/Users/anorris9/Library/CloudStorage/OneDrive-Humana/Desktop/Capstones/vueInstagramCapstone/vueInstagramCapstone/src/assets/messsage.png"
        alt=""
      />
      <img
        class="save"
        src="/Users/anorris9/Library/CloudStorage/OneDrive-Humana/Desktop/Capstones/vueInstagramCapstone/vueInstagramCapstone/src/assets/save.png"
        alt=""
      />
    </div>

    <div class="userPost">
      <p class="userNamePost">{{ profile.username }}</p>
      <p class="loremIpsum">{{ profile.caption }}</p>
    </div>
  </div>
</template>

<style scoped>
.igCardContainer {
  width: 600px;
  border: solid 1px lightgray;
  display: flex;
  flex-direction: column;
  padding-top: 20px;
  padding-bottom: 20px;
  margin: 20px;
  border-radius: 1%;
}

.userInfo {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.profilePic {
  height: 75px;
  width: 75px;
  border-radius: 60%;
  border: hotpink solid 2px;
  margin-left: 5px;
}

.userName {
  font-weight: bold;
  padding-left: 20px;
}

.kebab {
  display: flex;
  flex-direction: row;
  padding-left: 300px;
}
/* FIX THE SPACING */

.imagePosted {
  margin-top: 10px;
  width: 600px;
}

.likesContainer {
  display: flex;
  flex-direction: row;
  padding: 5px;
  margin-top: 10px;
}

.likes {
  margin-left: 5px;
  margin-top: 5px;
  display: flex;
  flex-direction: row;
}
.comment {
  height: 35px;
  margin-left: 20px;
}

.message {
  height: 35px;
  margin-left: 20px;
}

.save {
  align-content: end;
  height: 35px;
  margin-left: 350px;
}
.heartsContainer {
  padding-top: 17px;
}

.unfilledHeart {
  height: 35px;
}

.filledHeart {
  height: 35px;
}

.userNamePost {
  font-weight: bold;
  margin-left: 15px;
  margin-right: 15px;
}
.loremIpsum {
  margin-left: 15px;
  margin-right: 15px;
}
</style>

<!-- 
//PUT -> update an item in the database
fetch(`https://66b616b1b5ae2d11eb65dc8f.mockapi.io/items/${item.id}`, options)
.then(response => {
  return response.json()
})
.then(data => {
//makes sure that our item in code matches changes to item in database
item.inCart = data.inCart
})
} -->
