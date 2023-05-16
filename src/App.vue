<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: Date.now(),
          content: "Postar aqui é muito legal",
        },
        {
          title: "Meu segundo post",
          datetime: Date.now(),
          content: "Postar aqui não é tão legal",
        },
      ],
      FormData: {
        title: "",
        content: "",
      },
    };
  },
  methods: {
    handleClick(event) {
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
      this.posts.push({
        title: this.FormData.title,
        content: this.FormData.content,
        datetime: dataDaPostagem,
      });

      this.FormData = {
        title: "",
        content: "",
      };
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
  <div id="lista-posts">
    <div class="post" v-for="post in posts" :key="post.title">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

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
    <button class="learn-more" type="button" @click="handleClick">Criar</button>
  </form>

  <RouterView />
</template>

<style scoped>
* {
  font-family: "Poppins", sans-serif;
  max-width: 80%;
}

#lista-posts, form {
  margin: 0 auto;
  max-width: 50%;
}

#lista-posts {
  padding-left: 5rem ;
}

form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

form > * {
  margin: 1rem;
  display: flex;
  width: 100%;

  border: 1.9px solid #b18597;
}

::placeholder{
  color: #382b22;
}

button > * {
  box-sizing: border-box;
  font-family: "Rubik", sans-serif;
}

button > ::before,
::after {
  box-sizing: border-box;
}

button {
  font-family: "Rubik", sans-serif;
  font-size: 1rem;
  line-height: 1.5;
  display: flex;
  align-items: center;
  justify-content: center;
  
  max-width: 20vh;
  max-height: 20vh;
  background: #fff;

  position: relative;
  display: inline-block;
  cursor: pointer;
  outline: none;
  border: 0;
  vertical-align: middle;
  text-decoration: none;
  font-size: inherit;
  font-family: inherit;
}

.learn-more {
  font-weight: 700;
  color: #382b22;
  text-transform: uppercase;
  padding: 1.25em 2em;
  background: #fff0f0;
  border: 2px solid #b18597;
  border-radius: 0.75em;
  transform-style: preserve-3d;
  transition: transform 150ms cubic-bezier(0, 0, 0.58, 1),
    background 150ms cubic-bezier(0, 0, 0.58, 1);
}

button::before {
  position: absolute;
  content: "";
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #f9c4d2;
  border-radius: inherit;
  box-shadow: 0 0 0 2px #b18597, 0 0.625em 0 0 #ffe3e2;
  transform: translate3d(0, 0.75em, -1em);
  transition: transform 150ms cubic-bezier(0, 0, 0.58, 1),
    background 150ms cubic-bezier(0, 0, 0.58, 1);
}

button:hover {
  background: #ffe9e9;
  transform: translate(0, 0.25em);
}

button:hover::before {
  box-shadow: 0 0 0 2px #b18597, 0 0.5em 0 0 #ffe3e2;
  transform: translate3d(0, 0.5em, -1em);
}

button:active {
  background: #ffe9e9;
  transform: translate(0em, 0.75em);
}

button:active::before {
  box-shadow: 0 0 0 2px #b18597, 0 0 #ffe3e2;
  transform: translate3d(0, 0, -1em);
}
</style>
