<script>
import { RouterLink } from "vue-router";
export default {
  props: {
    posts: Array,
  },
  data() {
    return {
      search: "",
      showModal: false,
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
  methods: {
    getPostId(title) {
      //passa pela lista de posts (não filtrada)
      for (const index in this.posts) {
        //acessa o post na posição index da lista de posts
        const post = this.posts[index];
        //verifica se o título do post atual é igual ao título buscado
        if (post.title === title) return index;
      }
    },
    toggle() {
      this.showModal = !this.showModal
    },
  },
};
</script>

<template>
  <input
    id="search"
    v-model="search"
    @input=""
    placeholder="Procure pelo título do post..."
  />

  <div id="lista-posts">
    <div class="post" v-for="post in filteredPosts" :key="post.title">
      <h5>{{ post.datetime }}</h5>
      <h3>
        {{ post.title }}
      </h3>
      <p>
        {{ post.content
        }}<RouterLink :to="`/edit/${getPostId(post.title)}`">
          <span class="material-symbols-rounded"> edit </span>
        </RouterLink>
      </p>
      <span class="material-symbols-outlined" @click="toggle"> delete </span>
    </div>
  </div>
  <div class="modal" v-show="showModal">
    <div class="modal-content">
      <h3>Deletar Post</h3>
      <p>Tem certeza que quer deletar o post "TITULO DO POST"?</p>

      <div class="modal-actions">
        <button class="btn-cancelar" @click="toggle">cancelar</button>
        <button class="btn-confirmar">confirmar</button>
      </div>
    </div>
  </div>
</template>

<style></style>
