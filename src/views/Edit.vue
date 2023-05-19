<script>
import PostForm from "@/components/PostForm.vue";
export default {
  props: {
    posts: Array,
  },
  data() {
    //acessa o parâmetro id uma única vez
    const id = this.$route.params.id;
    return {
      //expondo a variável id para ser acessível
      id: id,
      post: this.posts[id],
      //recebe o post como um props
      // retorna o post a partir do parametro da rota, a partir do botaozinho de cada post que tem um id especifico, e o id é um parametro
      //post: this.posts[id],  -----> foi substituio pelo de cima
    };
  },
  components: {
    PostForm,
  },
};
</script>

<template>
  <PostForm :post="post" :id="id" />
</template>
