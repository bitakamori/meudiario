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
      selectedPost: null,
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
    setupModal(id) {
      // mostrar e esconder o modal
      this.showModal = !this.showModal;
      //selecionar o post e desselecionar o post
      if (id) {
        this.selectedPost = this.posts[id]; //salva o post inteiro (com titulo, conteudo e data)
        return;
      }
      this.selectedPost = null;
    },
    deletePost() {
      const id = this.getPostId(this.selectedPost.title);
      this.$emit("delete-post", id);
      //feche o modal e desselecione o p post
      this.setupModal();
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
    <div class="flex">
      <RouterLink :to="`/detail/${getPostId(post.title)}`">
        <h3 class="title">
        {{ post.title }}
      </h3>
      </RouterLink>
      <RouterLink :to="`/edit/${getPostId(post.title)}`">
          <span id="span1" class="material-symbols-rounded"> edit </span>
        </RouterLink>
      <span 
        id="span2" class="material-symbols-outlined"
        @click="setupModal(getPostId(post.title))"
      >
        delete
      </span>
    
    </div>
     
      <h5>{{ post.datetime }}</h5>
      <p>
        {{ post.content}}
        </p>
    </div>
  </div>
  <div class="modal" v-show="showModal">
    <div class="modal-content">
      <h3>Deletar Post</h3>
      <p>Tem certeza que quer deletar o post '{{ selectedPost?.title }}'?</p>

      <div class="modal-actions">
        <button class="btn-cancelar" @click="setupModal">cancelar</button>
        <button class="btn-confirmar" @click="deletePost">confirmar</button>
      </div>
    </div>
  </div>
</template>

<style>
.spans {
  display: flex;
  justify-content: space-evenly;
  

  width: 50%;

  margin: 0 auto;
  margin-bottom: 5rem;
}
</style>
