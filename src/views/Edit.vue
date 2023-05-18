<script>
import PostForm from "@/components/PostForm.vue";
export default {
  props: {
    posts: Array,
  },
  data() {
    return {
      //recebe o post como um props
      // retorna o post a partir do parametro da rota, a partir do botaozinho de cada post que tem um id especifico, e o id é um parametro
      post: this.posts[this.$route.params.id],
    };
  },
  components: {
    PostForm,
  },
};
</script>

<template>
  <PostForm :post="post"/>
</template>
