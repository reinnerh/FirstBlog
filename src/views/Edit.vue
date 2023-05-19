<script>
import PostForm from '../Components/PostForm.vue';
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
   components: {
    PostForm,
  },
};
</script>

<template>
<PostForm :post="post" :id="id"/>
</template>
