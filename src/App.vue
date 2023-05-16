<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Titulo",
          datetime: Date.now(),
          content: "Conteudo bacana!",
        },
        {
          title: "Outro titulo",
          datetime: Date.now(),
          content: "Conteudo não tão bacana!",
        },
      ],
      formData: {
        title: "",
        content: "",
        /*para pegar as infos colocadas*/
      },
      search: "",
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
    handleClick(event) {
      console.log(this.formData);

      //adicionar o post para lista de posts:
      const now = new Date();
      const dataDaPostagem = `${now.getDate()}/${
        now.getMonth() + 1
      }/${now.getFullYear()}`;

      //metodo 1:
      /* this.posts[this.posts.length] = {
        title: this.formData.title,
        content: this.formData.content,
      } */
      //metodo 2:
      this.posts.push({
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      });

      this.formData = {
        title: "",
        content: "",
      };
    },
    handleInputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
    /* para tratar os inputs */
  },
};
</script>

<template>
  <input v-model="search" placeholder="Procure pelo título do post..." />
  <div id="lista-posts">
    <div class="post" v-for="x in filteredPosts" :key="posts.title">
      <h3>{{ x.title }}</h3>
      <h4>{{ x.datetime }}</h4>
      <p>{{ x.content }}</p>
    </div>
  </div>

  <form>
    <!-- <input :value="text" @input="event => text = event.target.value"> -->
    <input v-model="formData.title" placeholder="Título" />
    <textarea
      v-model="formData.content"
      placeholder="Escreva seu post aqui..."
      rows="10"
      cols="50"
    ></textarea>
    <button type="button" @click="handleClick">Criar</button>
  </form>

  <RouterView />
</template>

<style scoped>
#lista-posts {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.post {
  height: 150px;
  width: 300px;
  margin: 10px;
}

form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

form > * {
  margin: 1rem;
  border-color: transparent;
}
</style>
