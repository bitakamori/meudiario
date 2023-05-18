<script>
export default {
  data() {
    return {
      FormData: {
        title: "",
        content: "",
      },
    };
  },
  methods: {
    handleClick(event) {
      if (!this.FormData.title){
        alert("preencha o título do post");
        return; 
      }
      //adicionar o posta à lista de posts
      const now = new Date();
      const dataDaPostagem = `${now.getDate()}/${
        now.getMonth() + 1
      }/${now.getFullYear()}`;

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

      const newPost = {
        title: this.FormData.title,
        content: this.FormData.content,
        datetime: dataDaPostagem,
      };
      //emite o evento creat-post
      this.$emit("create-post", newPost);

      this.FormData = {
        title: "",
        content: "",
      };
      this.$router.push("/");
    },
    handleInputChange(event) {
      const { name, value } = event.target;
      // essa função de cima é igual fazer essa de baixo só q mais sucinto.
      // event.target.name
      // event.target.value

      this.FormData[name] = value;
    },
  },
};
</script>

<template>
  <form action="">
    <!-- essa @keyup = handleInputChange é pra trata os inputs que coloca nos campos pra nao cuidar td de uma vez quando da submit. -->
    <input name="title" v-model="FormData.title" placeholder="Título" />
    <textarea
      name="content"
      :value="FormData.content"
      @keyup="handleInputChange"
      id=""
      cols="30"
      rows="10"
      placeholder="Escreva seu post aqui ..."
    ></textarea>

    <button class="learn-more" type="button" @click="handleClick">Criar Post</button>
  
  </form>
</template>

<style></style>
