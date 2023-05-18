<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";

export default {
  data() {
    return {
      posts: [
        // title= "titulo",
        // content= "texto textotexto textotexto textotexto textotexto textotexto textotexto textotexto texto"

      ],
    };
  },
  methods: {
    addPost(newPost) {
      //adicionar o novo post à lista de posts
      this.posts.push(newPost);
    },
  },
};
</script>

<template>
<header>
    <nav>
      <RouterLink to="/"> Home </RouterLink>
      <RouterLink to="/create"> Novo Post</RouterLink>
    </nav>
  </header>

  <main>
    <RouterView :posts="posts" @create-post="addPost" />
  </main>
  <footer>
    <img id="gif" src="cat.gif" />
  </footer>
</template>

<style scoped>
header{
  /* background: red; */
  display: flex;
  justify-content: center;
}

nav {
  /* background: blue; */
  margin-top: 1rem;
  width: 20%;
  display: flex;
  justify-content: space-around;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}


</style>
