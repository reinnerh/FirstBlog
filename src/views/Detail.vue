<script>
export default {
  props: {
    posts: Array,
  },
  data(){
    const idData = this.$route.params.id;
    return {
      id: idData,
      post: this.posts[idData]
    }
  },
};
</script>
<template>
  <main>
    <h2>{{ post.title }}</h2>
    <h4>{{ post.datetime }}</h4>
    <textarea readonly :value="post.content" rows="10" cols="50"></textarea>
  </main>
</template>

<style scoped>
textarea {
  resize: none;
  outline: none;
  border: black;
  border-radius: 10px;
  justify-content: center;
  align-items: center;
  text-align: center;
  width: 80%;
  height: 100%;
}

main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
