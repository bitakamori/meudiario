<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";

export default {
  data() {
    return {
      posts: [
        {
          datetime: "18/5/2023",
          title: "titulo muito grande demais very very",
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
    removePost(id) {
      //pode usar o slice sem ter q fazer td isso, mas isso mostra o q acontece por debaixo dos panos do slice
      //como remover um post do array this.posts
      const minhaNovaLista =[];
      for (const index in this.posts) {
        if (index == id) {
          continue;
        }
        const post = this.posts[index];
        minhaNovaLista.push(post);
      }
      this.posts = minhaNovaLista;
    }
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
    <RouterView :posts="posts" @create-post="addPost" @edit-post="updatePost" @delete-post="removePost"/>
  </main>

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
