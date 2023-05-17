<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";
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
  <input id="search" v-model="search" placeholder="Procure pelo título do post..." />
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
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px;
  margin-top: 20px;
  border-radius: 10px;
}

form > * {
  margin: 1rem;
  border: none;
  outline: none;
  padding: 10px;
  font-size: 16px;
  border-radius: 10px;
  width: 100%;
  transition: all 0.3s ease-in-out;
}

form > input:focus,
form > textarea:focus {
  border: 5px solid #ccc;
}

form button {
  background-color: #30629c;
  color: #fff;
  font-size: 16px;
  padding: 10px 20px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
}

form button:hover {
  background-color: #659bd1;
}

#search {
  padding: 10px;
  font-size: 13px;
  border: 2px solid #ccc;
  border-radius: 10px;
  width: 20%;
  transition: all 0.5s ease-in-out;
}

#search:focus {
  border: 2px solid #0077ff;
  background-color: #6e88a7;
}
</style>
