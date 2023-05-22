<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";
export default {
  data() {
    return {
      posts: [
        {
          title: "Primeiro Post",
          datetime: "23/08/476d.C",
          content: "Odoacro se autoproclamou o primeiro rei da Itália.",
        },
        {
          title: "Segundo Post",
          datetime: "29/05/1453",
          content: "Mehmed II finaliza o cerco de Constantinopla.",
        },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      //adicionar um novo post a lista de posts
      this.posts.push(newPost);
    },
    updatePost(updatePost, id) {
      this.posts[id] = updatePost;
    },
    removePost(id) {
      this.posts.splice(id,1)

/*       //metodo 2
      for (const index in thisposts) {
       if (index == id) {
        continue;
       }
       const post = this.posts[index];
       minhaNovaLista.push(post);
      }
      this.posts = minhaNovaLista; */
    }
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

  <main>
    <RouterView :posts="posts" @create-post="addPost" @edit-post="updatePost" @delete-post="removePost" />
  </main>
</template>

<style scoped>
nav {
  display: flex;
  justify-content: space-around;
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
