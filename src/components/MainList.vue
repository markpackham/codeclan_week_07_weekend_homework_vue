<template>
  <div class="list">
    <h2>Select a film</h2>
    <div>
      <select v-on:change="handleSelect" v-model="selectedFilm">
        <option v-for="(film, index) in films" :key="index" :value="film">{{film.title}}</option>
      </select>
    </div>

    <h3>Your favourite films</h3>
    <div v-if="selectedFilm">
      <button
        v-if="!favFilms.includes(selectedFilm)"
        v-on:click="addToFav"
      >Add: {{selectedFilm.title}} to favourites</button>

      <h4>Favourite films list</h4>
      <ul>
        <li v-for="(film, index) in favFilms" :film="film" :key="index">
          {{film.title}}
          <button
            class="btn-danger"
            v-on:click="removeFav(film)"
          >Remove: {{film.title}}</button>
        </li>
      </ul>
      <button class="btn-danger" v-on:click="removeAllFavs()">Remove All Favs</button>
    </div>

    <h3>All Films</h3>
    <div>
      <ol>
        <li v-for="(film, index) in films" :film="film" :key="index">{{film.title}}</li>
      </ol>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "main-list",
  data() {
    return {
      selectedFilm: {},
      favFilms: []
    };
  },
  props: ["films"],
  methods: {
    handleSelect() {
      eventBus.$emit("film-selected", this.selectedFilm);
    },
    addToFav() {
      this.favFilms.push(this.selectedFilm);
    },
    removeFav(film) {
      this.favFilms.splice(this.favFilms.indexOf(film), 1);
    },
    removeAllFavs() {
      this.favFilms = [];
    }
  }
};
</script>

<style>
</style>