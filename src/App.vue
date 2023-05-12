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
    };
  },
  methods: {
    handleClick(event){
      event.preventDefault();
    }
  }
};
</script>

<template>
  <div id="lista-posts">
    <div class="post" v-for="x in posts" :key="posts.title">
        <h3>{{x.title}}</h3>
        <h4>{{ x.datetime }}</h4>
        <p>{{ x.content }}</p>
    </div>
  </div>

  <form action="">
    <input name="title">
    <textarea name="content" id="" cols="" rows="10"></textarea>
    <button type="submit" @click="handle">Criar</button>
  </form>

  <RouterView />
</template>

<style scoped>

form {
  display: flex;
  flex-direction: column;

}

form > * {
  margin: 1rem;
}

</style>
