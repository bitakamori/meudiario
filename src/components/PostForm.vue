<script>
export default {
  props: {
    post: Object,
    id: String,
  },
  data() {
    return {
      FormData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
      },
      isEditing: Boolean(this.post),
    };
  },
  methods: {
    handleCreatPost(event) {
      if (!this.FormData.title) {
        alert("preencha o título do post");
        return;
      }
      //adicionar o posta à lista de posts
      const now = new Date();
      const dataDaPostagem = `${now.getDate()}/${
        now.getMonth() + 1
      }/${now.getFullYear()} - ${now.getHours()}:${now.getMinutes()}:${now.getSeconds()}`;

      // metodo 1
      // this.post[this.posts.length] = {
      //   title: this.FormData.title
      //   content: this;this.FormData.content
      // };

      // metodo 2
      //utilizou este metodo no inicio, que é igual ao metodo 1, mas era utili apenas quando o app tinha o codigo inteiro, agora q
      //separou as views ele mudou este metodo para salvar o post na view home
      // this.posts.push({
      //   title: this.FormData.title,
      //   content: this.FormData.content,
      //   datetime: dataDaPostagem,
      // });

      const PostData = {
        title: this.FormData.title,
        content: this.FormData.content,
        datetime: dataDaPostagem,
      };
      if (this.isEditing) {
        this.$emit("edit-post", PostData, this.id);
      } else {
        //emite o evento creat-post
        this.$emit("create-post", PostData);
      }
      //foi substituido pelo de cima talvez
      //   this.FormData = {
      //     title: "",
      //     content: "",
      //   };
      this.$router.push("/");
    },
  },
};
</script>

<template>
  <form action="">
    <input name="title" v-model="FormData.title" placeholder="Título" />
    <textarea
      v-model="FormData.content"
      cols="30"
      rows="10"
      placeholder="Escreva seu post aqui ..."
    ></textarea>

    <button class="btn" type="button" @click="handleCreatPost">
      Criar Post
    </button>
  </form>
</template>
