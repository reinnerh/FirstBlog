<script>
export default {
  data() {
    return {
      formData: {
        title: "",
        content: "",
        /*para pegar as infos colocadas*/
      },
    };
  },
  methods: {
    handleClick(event) {
      console.log(this.formData);


      if(!this.formData.title) {
        alert ("O Post precisa de um título!");
        return;
      }

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

      //emitir o evento create-post
      const newPost = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };


      this.$emit("create-post", newPost);

      this.formData = {
        title: "",
        content: "",
      };
      this.$router.push("/")
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
</style>
