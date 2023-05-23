<script>
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
};
</script>

<template>
  <div id="detail">
   
      <h3>
        {{ post.title }}
      </h3>
      <h5>{{ post.datetime }}</h5>
      <textarea class="detail-txt" readonly :value='post.content' >  </textarea>
   
 </div>
</template>

<style scoped>


</style>

