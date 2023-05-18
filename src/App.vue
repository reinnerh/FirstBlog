<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";
export default {
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    addPost(newPost) {
      //adicionar um novo post a lista de posts
      this.posts.push(newPost);
    },
  },
};
</script>

<template>
  <header>
    <nav>
      <RouterLink to="/" class="nav-link">Home</RouterLink>
      <RouterLink to="/create" class="nav-link">Novo Post</RouterLink>
    </nav>
  </header>

  <RouterView :posts="posts" @create-post="addPost" />
</template>

<style scoped>
nav {
  display: flex;
  justify-content: space-evenly;
}

.nav-link {
  display: inline-block;
  padding: 10px 20px;
  margin-top: 10px;
  font-size: 16px;
  text-decoration: none;
  color: #333;
  background-color: #dddddd;
  border-radius: 5px;
  transition: background-color 0.3s ease-in-out;
}

.nav-link:hover {
  background-color: #6e88a7;
}
</style>
