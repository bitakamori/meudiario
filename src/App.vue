<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";

export default {
  data() {
    return {
      posts: [
        {
          datetime: "18/5/2023",
          title: "titulo",
          content:
            "texto textotexto textotexto textotexto textotexto textotexto textotexto textotexto texto",
        },
        {
          datetime: "18/5/2023",
          title: "titulo2",
          content:
            "texto textotexto textotexto textotexto textotexto textotexto textotexto textotexto texto",
        },
      ],
    };
  },
  methods: {
    addPost(PostData) {
      //adicionar o novo post à lista de posts
      this.posts.push(PostData);
    },
    updatePost(updatePost, id) {
      // console.log(updatePost, id);
      this.posts[id] = updatePost;
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
    <RouterView :posts="posts" @create-post="addPost" @edit-post="updatePost" />
  </main>

  <footer>
    <img id="gif" src="cat.gif" />
  </footer>
</template>

<style scoped>
header {
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
