<script>
export default {
  props: {
    posts: Array,
  },
  data() {
    return {
      search: "",
    };
  },
  computed: {
    filteredPosts() {
      // se search estiver vazio, retorne a lista completa de posts
      if (!this.search) return this.posts;

      // se tiver qualquer coisa em search, faz o filtro
      const listaFinal = [];
      for (const post of this.posts) {
        if (post.title.includes(this.search)) {
          listaFinal.push(post);
        }
      }
      return listaFinal;
    },
  },
};
</script>

<template>
  <input
    v-model="search"
    @input=""
    placeholder="Procure pelo título do post..."
  />

  <div id="lista-posts">
    <div class="post" v-for="post in filteredPosts" :key="post.title">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>
</template>

<style>
#lista-posts {
  margin: 0 auto;
  max-width: 50%;
    /* padding-left: 15rem; */
    background: #f9c4d2;
  position: relative;
  /* text-align: center; */
}

#lista-posts:after {
  content: "";
  display: block;
  position: absolute;
  width: 100%;
  height: 29px;
  right: 0;
  bottom: -25px;
  left: 0;
  background: linear-gradient(#f9c4d2 50%, rgba(255,255,255,0) 0) 0 0,
  radial-gradient(circle closest-side, #f9c4d2 53%, rgba(255, 255, 255, 0) 0) 0 0,
    radial-gradient(circle closest-side, #f9c4d2 50%, rgba(255, 255, 255, 0) 0)
      25px 0 white;
      background-size: 110px 200px;
background-repeat: repeat-x;
  background-position: center;
}

</style>
