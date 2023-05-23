<script>
export default {
  props: {
    post: Object,
    id: String,
  },

  data() {
    return {
      formData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
        /*para pegar as infos colocadas*/
      },
      editable: Boolean(this.post),
      buttonText: Boolean(this.post) === true ? "Editar Post" : "Criar Post",
    };
  },
  methods: {
    handleCreatePost(event) {
      console.log(this.formData);

      if (!this.formData.title) {
        alert("O Post precisa de um título!");
        return;
      }

          //cria constantes e adiciona padStart com 2 para garantir que tenha dois digitos se não coloca um 0 na esquerda
      const now = new Date();
      const day = now.getDate().toString().padStart(2, "0");
      const mes = (now.getMonth() + 1).toString().padStart(2, "0");
      const ano = now.getFullYear();
      const horas = now.getHours().toString().padStart(2, "0");
      const minutos = now.getMinutes().toString().padStart(2, "0");

      const dataDaPostagem = `${day}/${mes}/${ano} - ${horas}:${minutos}`;

      //metodo 1:
      /* this.posts[this.posts.length] = {
        title: this.formData.title,
        content: this.formData.content,
      } */

      const objPost = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };

      if (this.editable) {
        this.$emit("edit-post", objPost, this.id);
      } else {
        this.$emit("create-post", objPost);
      }

      this.formData = {
        title: "",
        content: "",
      };
      this.$router.push("/");
    },
  },
};
</script>

<template>
  <form>
    <!-- <input :value="text" @input="event => text = event.target.value"> -->
    <input v-model="formData.title" placeholder="Título" />
    <textarea
      v-model="formData.content"
      placeholder="Escreva seu post aqui..."
      rows="10"
      cols="50"
    ></textarea>

    <button type="button" @click="handleCreatePost">{{ buttonText }}</button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px;
  margin-top: 20px;
  border-radius: 10px;
}

form > input {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  width: 30%;
}

form > * {
  margin: 1rem;
  border: none;
  outline: none;
  padding: 10px;
  font-size: 16px;
  border-radius: 10px;
  width: 100%;
  background-color: white;
  transition: all 0.3s ease-in-out;
}

form > input:focus,
form > textarea:focus {
  border: 5px solid #ccc;
  background-color: white;
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
</style>
