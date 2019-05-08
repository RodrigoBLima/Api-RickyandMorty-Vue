<template>
  <div id="app">
    <div class="hero is-white is-gradient is-bold">
      <div class="hero-body">
        <h1 class="title">
          <span class="has-text-success">Rick and Morty</span>
          <span class="subtitle">Personagens</span>
        </h1>
        <button class="button is-success is-rounded" v-on:click="fetch">aaaaa</button>
      </div>
    </div>

    <div class="container">
      <div class="columns is-desktop is-mobile is-tablet is-multiline is-centered">
        <div
          class="column is-12-mobile is-4-desktop is-4-tablet"
          v-for="character of characters"
          v-bind:key="character.id"
        >
          <div class="card">
            <div class="card-header">
              <img v-bind:src="character.image" v-vind:alt="character.name">
            </div>
            <div class="card-content">
              <h3 class="title is-size-4">{{ character.name }}</h3>
              <button class="button is-success is-rounded is-small">Ver Mais</button>
            </div>
          </div>
        </div>
      </div>
      <nav class="pagination" role="navigation" aria-label="pagination">
        <a class="pagination-previous" v-on:click="changePage( page -1)">Anterior</a>
        <ul class="pagination-list">
          <li>
            <a class="pagination-link is-current">{{ page }}</a>
          </li>
        </ul>
        <a class="pagination-next" v-on:click="changePage( page +1)">Próximo</a>
      </nav>
    </div>
  </div>
</template>

<script>
// bibliotecas
import axios from "axios";
//import Character from "./components/Character";

export default {
  name: "App",
  //components: [Character],
  data() {
    return {
      characters: [],
      page: 1,
      pages: 1
    };
  },
  created() {
    this.fetch();
  },
  methods: {
    fetch() {
      const paramn = {
        page: this.page
      };
      let result = axios
        .get("https://rickandmortyapi.com/api/character", { paramn })
        .then(res => {
          this.characters = res.data.results;

          this.pages = res.data.info.pages;
          console.log(res.data);
        })
        .catch(err => {
          console.log(err);
        });
    },
    chengePage(page) {
      this.ṕage = page <= 0 || page > this.pages ? this.page : page;
      this.fetch();
    }
  }
};
</script>

