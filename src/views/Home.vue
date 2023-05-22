<script>
import { RouterLink } from "vue-router";
export default {
  props: {
    posts: Array,
  },
  data() {
    return {
      search: "",
      showModal: false,
      selectedPost: null,
    };
  },
  computed: {
    filteredPosts() {
      //se search estiver vazio, retorne a lista completa de posts
      if (!this.search) return this.posts;

      //se tiver qualquer coisa em search, faz o filtro
      const listaFinal = [];
      for (const post of this.posts) {
        if (post.title.includes(this.search)) {
          listaFinal.push(post);
        }
      }
      return listaFinal;
    },
  },
  methods: {
    getPostID(title) {
      //passa pela lista de posts(não filtrada)
      for (const index in this.posts) {
        //acessa o post na posição index da lista de posts
        const post = this.posts[index];

        //verifica se o título do post atual é igual ao titulo buscado
        if (post.title === title) return index;
      }
    },
    setupModal(id) {
      this.showModal = !this.showModal;

      if (id) {
        this.selectedPost = this.posts[id];
        return;
      }

      this.selectedPost = null;
    },
    deletePost() {
      const id = this.getPostID(this.selectedPost.title);
      this.$emit("delete-post",id);
      this.setupModal()
    }
  },
};
</script>

<template>
  <input
    id="search"
    v-model="search"
    placeholder="Procure pelo título do post..."
  />
  <div id="lista-posts">
    <div class="post" v-for="x in filteredPosts" :key="posts.title">
      <h3>
        {{ x.title }}
        <RouterLink :to="`/edit/${getPostID(x.title)}`">
          <span class="material-symbols-rounded">edit</span>
        </RouterLink>
        <span
          class="material-symbols-rounded"
          @click="setupModal(getPostID(x.title))"
          >delete</span
        >
      </h3>
      <h4>{{ x.datetime }}</h4>
      <p>{{ x.content }}</p>
    </div>
  </div>
  <div class="modal" v-show="showModal">
    <div class="modal-content">
      <h3>{{ selectedPost?.title }}</h3>
      <p>Tem certeza que deseja deletar esse post?</p>

      <div class="modal-actions">
        <button class="bg-error" @click="setupModal">Cancelar</button>
        <button class="bg-success" @click="deletePost" >Confirmar</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
#lista-posts {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  text-align: center;
  gap: 20px;
}

.post {
  margin-top: 1rem;
  height: 150px;
  width: 400px;
  padding: 20px;
  border: 2px solid #ccc;
  border-radius: 10px;
  transition: all 0.3s ease-in-out;
  overflow: auto;
}

.post:hover {
  transform: translateY(-5px);
  background-color: rgb(193, 226, 255);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

#search {
  display: block;
  margin: auto;
  padding: 10px;
  font-size: 13px;
  border: 2px solid #ccc;
  border-radius: 10px;
  width: 20%;
  transition: all 0.5s ease-in-out;
}

#search:focus {
  border: 2px ridge #53a3ff;
  background-color: rgb(193, 226, 255);
}
</style>
