<template>
  <div>
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